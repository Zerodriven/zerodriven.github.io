---
layout: single
date: 2026-05-22
categories: Azure, DotNet
classes: wide
---
Scenario: Got several hundred unmanaged guest accounts in Azure and I hate PowerShell. This is not production ready, but it can be converted quite easily to an Azure Function and moved into Azure Automation. Graph permissions are needed.

Script can be run as part of a solution (Make sure to download the relevant NuGet packages for the relevant imports) and with dotnet run.

The script should run weekly.

1. Run the script: It marks all guest accounts as disabled if they've not logged in within 6 months
2. Run it again, it deletes them.

```csharp
using Azure.Identity;
using Microsoft.Graph;
using Microsoft.Graph.Models;
using Microsoft.Graph.Models.ODataErrors;

var tenantId = "";
var clientId = "";
var clientSecret = "";

var credential = new ClientSecretCredential(tenantId, clientId, clientSecret);
var graphClient = new GraphServiceClient(credential);

var sixMonthsAgo = DateTimeOffset.UtcNow.AddMonths(-6);

Console.WriteLine("Starting user scorched earth...");

// 1. Initial Request (The SDK will only fetch the first page, usually 100 users)
var usersResponse = await graphClient.Users.GetAsync(config =>
{
    config.QueryParameters.Filter = "userType eq 'Guest'";
    config.QueryParameters.Select = ["id", "displayName", "accountEnabled", "signInActivity", "createdDateTime"];
});

// 2. Use PageIterator to handle all users
var pageIterator = PageIterator<User, UserCollectionResponse>.CreatePageIterator(
    graphClient,
    usersResponse,
    async (user) =>
    {
        try
        {
            // ACTION A: PURGE DISABLED
            if (user.AccountEnabled == false)
            {
                await graphClient.Users[user.Id].DeleteAsync();
                Console.WriteLine($"[PURGED] {user.DisplayName}");
                return true; // Continue to next user
            }

            // ACTION B: DISABLE INACTIVE
            var lastSignIn = user.SignInActivity?.LastSignInDateTime;
            var createdDate = user.CreatedDateTime;

            bool isInactive = (lastSignIn.HasValue && lastSignIn < sixMonthsAgo) || 
                              (!lastSignIn.HasValue && createdDate < sixMonthsAgo);

            if (isInactive && user.AccountEnabled == true)
            {
                await graphClient.Users[user.Id].PatchAsync(new User { AccountEnabled = false });
                Console.WriteLine($"[DISABLED] {user.DisplayName}");
            }
        }
        catch (ODataError ex) { Console.WriteLine($"Error on {user.DisplayName}: {ex.Error?.Message}"); }
        
        return true; // Always return true to keep the iterator moving
    });

await pageIterator.IterateAsync();

Console.WriteLine("Done.");
```