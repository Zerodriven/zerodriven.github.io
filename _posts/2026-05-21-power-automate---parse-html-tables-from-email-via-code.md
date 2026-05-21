---
layout: single
date: 2026-05-21
categories: PowerAutomate
classes: wide
---
Scenario:

Frequently get an email with an embedded HTML table which requires parsing, however the email body technically contains two tables. One being a security banner (Which I didn't realise was a table) and one being the actual table we want to parse.

Now, there are a few good references already out there:

1. [Extract data from html table in email body](https://community.powerplatform.com/blogs/post/?postid=f6cc84fe-dcee-4b31-a576-4b6b11527791)
2. [Power Automate: Parse HTML Tables in Emails](https://medium.com/@jake.mannion/parsing-html-tables-from-incoming-email-via-power-automate-ce9daddcacaa)
3. [Extract HTML Table from Email in Power Automate – Advanced XML Process](https://www.powerplatformtip.com/article/powerplatform/2022/11/10/extract-html-table-email-power-automate/)
4. [Get data from HTML tables in Power Automate — Encodian](https://www.encodian.com/blog/get-data-from-html-tables-in-power-automate/)
5. [Extract data from html table from email body in Power Automate - Microsoft Power Platform](https://manish-solanki.com/extract-data-from-html-table-from-email-body-in-power-automate/)

However all of these require a lot more faffing around with formulas than I like, so what is my solution? Well, it's more pro-code and complex, but is re-usable. I've not tested it beyond two tables, especially if two tables both contain the same key, but this meets my initial need and is drastically faster than using 5x compose blocks within Power Automate.

1. Setup an Azure Function (parse-html) which is triggered via a HTTP request
2. Create a Power Automate flow which calls the API via a HTTP connector (POST)

Example data payload (Body of an Outlook email) - Values changed for privacy.

```json
        {
          "body": "<html><head>\r\n<meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf-8\"><style type=\"text/css\" style=\"display:none\">\r\n<!--\r\np\r\n\t{margin-top:0;\r\n\tmargin-bottom:0}\r\n-->\r\n</style></head><body dir=\"ltr\"><table border=\"1\" style=\"direction:ltr; background-color:rgb(239,245,158); width:100%; box-sizing:border-box; border-collapse:collapse; border-spacing:0px\"><tbody><tr><td style=\"direction:ltr; width:100%\"><div style=\"direction:ltr\"><b>EXTERNAL</b>: This email originates from outside of Jason Benedetti Network network. Be cautious with attachments and links!</div></td></tr></tbody></table><div style=\"direction:ltr\"><br><br><br></div><table cellspacing=\"0\" style=\"direction:ltr\"><tbody><tr><td style=\"direction:ltr\"><div id=\"x_x_o:go~r:reportResult\"><div id=\"x_x_o:go~r:report~v:compoundView!1ViewContainer\"><table cellspacing=\"0\" style=\"direction:ltr\"><tbody><tr><td align=\"center\" style=\"direction:ltr; vertical-align:top\"><table cellspacing=\"0\" style=\"direction:ltr; width:100%\"><tbody><tr><td align=\"center\" style=\"direction:ltr; vertical-align:top\"><div id=\"x_x_saw_240738_1_3\"><table cellspacing=\"0\" style=\"direction:ltr\"><tbody><tr><td style=\"direction:ltr\"><table id=\"x_x_saw_240738_1_5\" cellspacing=\"0\" style=\"direction:ltr\"><tbody><tr><td style=\"direction:ltr\"><div style=\"direction:ltr\">Person Number</div></td><td style=\"direction:ltr\"><div style=\"direction:ltr\">Name</div></td><td style=\"direction:ltr\"><div style=\"direction:ltr\">Process Date-Time</div></td><td style=\"direction:ltr\"><div style=\"direction:ltr\">Termination Date</div></td><td style=\"direction:ltr\"><div style=\"direction:ltr\">Assignment Type</div></td><td style=\"direction:ltr\"><div style=\"direction:ltr\">Legal Entity</div></td><td style=\"direction:ltr\"><div style=\"direction:ltr\">Position Code</div></td><td style=\"direction:ltr\"><div style=\"direction:ltr\">Level 05 Organization Name</div></td><td style=\"direction:ltr\"><div style=\"direction:ltr\">Position Name</div></td><td style=\"direction:ltr\"><div style=\"direction:ltr\">Job Name</div></td></tr><tr><td style=\"direction:ltr; text-align:left; vertical-align:top\"><div style=\"direction:ltr; text-align:left\">123456</div></td><td style=\"direction:ltr; text-align:left; vertical-align:top\"><div style=\"direction:ltr; text-align:left\">Benedetti, Jason</div></td><td style=\"direction:ltr; text-align:left; vertical-align:top\"><div style=\"direction:ltr; text-align:left\">06/05/2026 1:58 PM</div></td><td style=\"direction:ltr; text-align:left; vertical-align:top\"><div style=\"direction:ltr; text-align:left\">12/05/2026</div></td><td style=\"direction:ltr; text-align:left; vertical-align:top\"><div style=\"direction:ltr; text-align:left\">Employee</div></td><td style=\"direction:ltr; text-align:left; vertical-align:top\"><div style=\"direction:ltr; text-align:left\">Jason Benedetti Network</div></td><td style=\"direction:ltr; text-align:left; vertical-align:top\"><div style=\"direction:ltr; text-align:left\">123456</div></td><td style=\"direction:ltr; text-align:left; vertical-align:top\"><div style=\"direction:ltr; text-align:left\">Engineering</div></td><td style=\"direction:ltr; text-align:left; vertical-align:top\"><div style=\"direction:ltr; text-align:left\">CTO</div></td><td style=\"direction:ltr; text-align:left; vertical-align:top\"><div style=\"direction:ltr; text-align:left\">Marketing Head</div></td></tr></tbody></table></td></tr></tbody></table></div></td></tr></tbody></table></td></tr></tbody></table></div><div id=\"x_x_idStatePathDiv\"></div></div></td></tr></tbody></table></body></html>"
		}
```

Now, the fun bit here is also the name. Because the source system doesn't normalise, it's backwards (Benedetti, Jason) - So we also normalise that.

Payload:

```json
{
  "html": "@{triggerOutputs()?['body/body']}",
  "keyword": "Person Number"
}
```

Azure function code: 

```python
import azure.functions as func
import json
from bs4 import BeautifulSoup

app = func.FunctionApp()

@app.route(route="parse-html", auth_level=func.AuthLevel.FUNCTION)
def parse_html(req: func.HttpRequest) -> func.HttpResponse:
    try:
        body = req.get_json()
        html = body.get("html", "")
        target_keyword = body.get("keyword", "Person Number").lower()

        soup = BeautifulSoup(html, "html.parser")
        tables = soup.find_all("table")

        target_rows = []

        for table in tables:
            if target_keyword not in table.get_text().lower():
                continue

            rows = table.find_all("tr")
            if not rows:
                continue

            headers = [th.get_text(strip=True) for th in rows[0].find_all(["td", "th"])]

            for tr in rows[1:]:
                cols = [td.get_text(strip=True) for td in tr.find_all(["td", "th"])]
                if cols and len(cols) == len(headers):
                    row_dict = dict(zip(headers, cols))

                    # --- Name Normalization Logic ---
                    name_key = next((k for k in row_dict if "name" in k.lower()), None)

                    if name_key and "," in row_dict[name_key]:
                        parts = [p.strip() for p in row_dict[name_key].split(",")]
                        if len(parts) == 2:
                            row_dict["Normalized Full Name"] = f"{parts[1]} {parts[0]}"
                        else:
                            row_dict["Normalized Full Name"] = row_dict.get(name_key, "")
                    # --------------------------------

                    target_rows.append(row_dict)

            if target_rows:
                break

        return func.HttpResponse(
            json.dumps({"success": bool(target_rows), "records": target_rows}),
            mimetype="application/json",
            status_code=200
        )

    except Exception as e:
        return func.HttpResponse(
            json.dumps({"error": str(e)}),
            mimetype="application/json",
            status_code=500
        )
```

How this works:

1. You pass the keyword you want to search on (Against the headers)
	1. If the keyword doesn't exist, it skips the table
	2. If it exists, it parses the columns and the values

Response payload if the keyword matches:

```json
{
    "body": {
        "success": true,
        "records": [
            {
                "Person Number": "123456",
                "Name": "Benedetti, Jason",
                "Process Date-Time": "06/05/2026 1:58 PM",
                "Termination Date": "12/05/2026",
                "Assignment Type": "Employee",
                "Legal Entity": "Jason Benedetti Network",
                "Position Code": "123456",
                "Level 05 Organization Name": "Jason Benedetti Network",
                "Position Name": "Engineering",
                "Job Name": "CTO",
                "Normalized Full Name": "Jason Benedetti"
            }
        ]
    }
}
```

Then you continue to do stuff with it!