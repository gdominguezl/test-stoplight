---
stoplight-id: umzn7bgkaju2z
---

# Endpoint 5 - Get client site reports

> **Description:** This endpoint retrieves the reports data for **one specific site ID associated with a client** and it only concerns about the reports array

Query params:
- `client`: Represents the client that owns a group of sites, for example: BRP, NIPSCO, SMT, etc.
- `siteId`: Represents a string with the ID of an specific client site. Example: Alvin (from the BRP client)
- `reportsTypes`: Used to filter charts within the reports object based on their "reportType" property. This property is matched for every chartType included in the reports object.
- `from`: Represents the start date of the requested summary data. (Format: MM-DD-YYYY)
- `to`: Represents the end date of the requested summary data. (Format: MM-DD-YYYY)

---

**Proposed endpoint**
```
/sites?client=<clientName>&siteId=<site_id>&reportsTypes=<report_type_1>,<report_type_2>,<report_type_n>&from=<dateFrom>&to=<dateUntil>
```

**Proposed JSON structure**

```json
{
  "client": "<client_name>",
  "sites": [
    {
      "id": "<site_id>",
      "title": "<site_title>",
      "reports": {
        "types": [
          "<report_type_1>",
          "<report_type_2>",
          "<report_type_n>",
        ],
        "charts": [
          // Chart types with the reportType specified at the endpoint [reportsTypes query param]
          {
            "chartType": "<chart_type>",
            "reportType": "<report_type_1>",
            "title": "<chart_title>",
            "xAxisTitle": "<x_axis_title>",
            "yAxisTitle": "<y_axis_title>",
            "xAxisLabels": ["<x_axis_label_1>", "<x_axis_label_2>"],
            "yAxisLabels": ["<y_axis_label_1>", "<y_axis_label_2>"],
            "data": [
              {
                "label": "<data_label>",
                "unit": "<data_unit>",
                "values": [
                  {
                    "x": "<x_value>",
                    "y": "<y_value>"
                  }
                ]
              }
            ]
          }
          // ...More chart types with the reportType specified at the endpoint [reportsTypes query param]
        ]
      },
    }
  ]
}

```

---