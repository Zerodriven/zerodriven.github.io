---
layout: single
date: 2026-05-26
categories: Engineering, Automation, PowerAutomate
classes: wide
---
Power Automate is fantastic at one thing: making it incredibly easy to build automation quickly.

It’s also fantastic at something else:  creating a mess of inconsistent, fragile, unmaintainable flows at scale. If you’ve been using Power Automate for a while, you’ve probably seen it:

- Flows with no error handling  
- Hardcoded URLs and email addresses everywhere  
- No logging or visibility  
- Broken processes no one wants to touch  
- “That one flow” only one person understands  

This isn’t a tooling problem.  It’s a governance problem.

It doesn't help that Microsoft doesn't make this easy and it doesn't help that there's no native default template for the product, so you have to do this every time, for every flow, for every environment and that drives me utterly insane.
# The Goal (What “Good” Looks Like)

A well-governed automation platform should produce flows that are:

- Consistent  
- Maintainable  
- Secure  
- Observable (you can debug them)  
- Reusable  

If your flows don’t meet those criteria, you’re building future operational debt.

# The Single Most Important Rule

Every flow should follow the same structure. Without that, nothing else matters.

# 1. Standard Flow Architecture

Every flow should follow this pattern:

    Trigger
    │
    ├── Scope: Initialisation
    ├── Scope: Main Logic (Try)
    ├── Scope: Error Handling (Catch)
    └── Scope: Finalisation (Finally)

## Why this matters

Most Power Automate issues aren’t logic bugs, they’re:

- Silent failures  
- Missing context  
- Lack of traceability  

This structure solves all of that.

## What each part does

### Initialisation

Set everything up centrally:

- Correlation ID
- Flow metadata
- Configuration references

Example:

```json
    {
      "flowName": "Example Flow",
      "correlationId": "@{guid()}",
      "startTime": "@{utcNow()}",
      "environmentName": "workflow().tags.environmentName OR as a dedicated variable"
    }
```
### Main Logic (Try)

This is your actual business logic:

- Keep it clean  
- Structure it into smaller scopes  
- Avoid deeply nested expressions  

Pattern:

    Scope - Main Logic
        Scope - Data Retrieval
        Scope - Processing
        Scope - Output
### Error Handling (Catch)

Runs when anything fails. Capture useful context:

```json
    {
      "status": "@{workflow().status}",
      "error": "@{workflow().error}",
      "correlationId": "@{guid()}"
    }
```

Actions should include:

- Logging the error  
- Sending notification (Teams / Email)  

No more silent failures.

### Finalisation (Finally)

Always runs regardless of success or failure.

Track completion:

    {
      "status": "@{workflow().status}",
      "endTime": "@{utcNow()}"
    }
# 2. Drop Hardcoding (Configuration Discipline)

Hardcoding is one of the biggest causes of pain. Instead:

## Use configuration layers

| Data Type            | Where it should live                                                        |
| :------------------- | :-------------------------------------------------------------------------- |
| **API URLs**         | Environment variables                                                       |
| **Email recipients** | Config list (SharePoint/Dataverse)                                          |
| **Site URLs**        | Environment variables                                                       |
| **Rule of thumb:**   | If you need to change it in more than one place, it shouldn't be hardcoded. |

## Rule of thumb

> If you need to change it in more than one place, it should not be hardcoded.

# 3. Naming Conventions

Naming isn’t just aesthetics. it’s operational clarity.

## Flows

    <Domain> - <Purpose>

Example:

    HR - Leavers Processing

## Variables

    varCamelCase

Example:

    varCorrelationId

## Actions

- Good: Get User Data  / GetUserData (To help with component lookups, removing underscores!)
- Bad: Action 1  

## Scopes

    Scope - <Purpose>

# 4. Error Handling is Not Optional

If your flow can fail (and it will), you need to handle it. At a minimum, every single flow must have a Try/Catch structure that captures the error message, timestamp, and Correlation ID, before notifying the team.

Think of it as an execution mindset shift. Instead of a user telling you, _"It failed once last week,"_ your system tells you, _"Flow X failed at 14:32 with error X, correlation ID Y, environment name Z."_

# 5. Logging = Observability

If you can't see what your flows are doing, you can't support them.

## Minimum logging events

- Start  
- Success  
- Failure  

## Minimum fields

- Flow name  
- Correlation ID  
- Status  
- Timestamp  
- Duration  
- Environment

## Where to log

Start simple:

- SharePoint list 
- Emails
- Automatically push errors into a ticketing system like Azure DevOps

Scale later:

- Dataverse  
- Application Insights  


# 6. Build for Reuse

Most teams rebuild the same logic repeatedly. Instead:

## Use child flows

Common reusable components:

- Logging  
- Notifications  
- API calls  
- Data transformations  

## Why bother?

- Change once updates everywhere  
- Keeps flows clean  
- Avoids duplication  

# 7. Templates Make This Stick

You can define standards all day, they won’t stick unless they’re easy to follow.

## Create a standard template

It should already include:

- Structured scopes  
- Error handling wired  
- Logging enabled  
- Naming conventions  

Then:

- Share it with your team  
- Make it the starting point  

## Reality check

Make the right way the easiest way.

# 8. Lightweight Governance

You don’t need heavy process.

## Pre-release checklist

- No hardcoded values  
- Error handling implemented  
- Logging enabled  
- Naming standards followed  
- Built inside a Solution  

That’s enough to massively improve quality.

# What's the point?

When applied correctly, you get:

- Fewer production issues  
- Faster debugging  
- Easier onboarding  
- Reusable patterns  
- Confidence to scale  

Most importantly: Your flows stop being scripts and become systems.

# Final Thought

Power Automate is powerful but without structure, it becomes chaos. Governance isn’t about slowing things down. It’s about ensuring what you build today is still understandable, fixable, and maintainable tomorrow. Also, why would we just not do this? Why does Microsoft not just make this the default for all user defined flows?

At the top I said you have to do this for every flow for every environment, always. One of my next blogs will show you how to get around that. Not perfectly, but something is better than nothing