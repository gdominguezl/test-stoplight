---
stoplight-id: b58ff4vk8h6f3
---

# Endpoint 1 - Get summary data by user authentication

> **Description:** This endpoint retrieves summary data for all sites that the current user has access to. The backend automatically determines which sites the user can access based on their organization and client session. Unlike **endpoint-3-get-all-sites-data-summary, which requires the user to specify the client**, this endpoint handles client detection internally.

Query params:
- `summaryList`: instructs the API to retrieve a summary of all sites.

---

**Proposed endpoint:**
```
/sites?summaryList
```

**Proposed JSON Structure:**
```json
[
  {
    "client": "<client_name>",
    "sites": [
      {
        "id": "<site_id>",
        "title": "<site_title>",
        "onlineRacks": "<online_racks>/<total_racks>",
        "status": "<site_status>",
        "upTime": "<site_uptime_percentage>",
        "batteryLevel": "<site_battery_level_percentage>",
        "generalMetrics": [
          {
            "id": "<metric_id>",
            "name": "<metric_name>",
            "units": "<metric_units>",
            "value": "<metric_value>"
          },
          // .. More metrics
        ],
        "reports": {
          "types": [
            "<report_type_1>", // To match with reportType key at charts array
            "<report_type_2>",
            "<report_type_n>",
          ],
          "charts": [
            {
              "chartType": "<chart_type>",
              "reportType": "<report_type_n>", // Should match with report > types
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
            // ...More chart types  
          ]
        },
      }
      // ...More sites 
    ]
  },
  {
    "client": "<client_name_2>",
    "sites": [
      {
        "id": "<site_id>",
        "title": "<site_title>",
        "onlineRacks": "<online_racks>/<total_racks>",
        "status": "<site_status>",
        "upTime": "<site_uptime_percentage>",
        "batteryLevel": "<site_battery_level_percentage>",
        "generalMetrics": [
          {
            "id": "<metric_id>",
            "name": "<metric_name>",
            "units": "<metric_units>",
            "value": "<metric_value>"
          },
          // .. More metrics
        ],
        "reports": {
          "types": [
            "<report_type_1>", // To match with reportType key at charts array
            "<report_type_2>",
            "<report_type_n>",
          ],
          "charts": [
            {
              "chartType": "<chart_type>",
              "reportType": "<report_type_n>", // Should match with report > types
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
            // ...More chart types  
          ]
        },
      }
      // ...More sites 
    ]
  },
]

```

---

**Example:**

Asuming that our user has access to BRP and SMT organizations, according to his organization code, get the summary data for all the sites within those organizations.

```
/sites?summaryList
```

**Mocked response (200)**

```json
[
  {
    "client": "BRP",
    "sites": [
      {
        "id": "alvin",
        "title": "Alvin",
        "onlineRacks": "4/4",
        "status": "Running",
        "upTime": "99%",
        "batteryLevel": "72%",
        "generalMetrics": [
          {
            "id": "net_energy_imported",
            "name": "Net Energy Imported",
            "units": "MWh",
            "value": 784.17
          },
          {
            "id": "net_energy_exported",
            "name": "Net Energy Exported",
            "units": "MWh",
            "value": 784.17
          },
          {
            "id": "net_throughput",
            "name": "Net Throughput",
            "units": "MWh",
            "value": 1504.78
          },
          {
            "id": "lifetime_throughput",
            "name": "Lifetime Throughput",
            "units": "MWh",
            "value": 26308.87
          }
        ],
        "reports": {
          "types": [
            "executive_summary",
            "cell_temperature",
            "cell_voltage",
          ],
        }
      },
      {
        "id": "angleton",
        "title": "Angleton",
        "onlineRacks": "0/4",
        "status": "Stopped",
        "upTime": "45%",
        "batteryLevel": "23%",
        "generalMetrics": [
          {
            "id": "net_energy_imported",
            "name": "Net Energy Imported",
            "units": "MWh",
            "value": 895.23
          },
          {
            "id": "net_energy_exported",
            "name": "Net Energy Exported",
            "units": "MWh",
            "value": 842.51
          },
          {
            "id": "net_throughput",
            "name": "Net Throughput",
            "units": "MWh",
            "value": 1737.74
          },
          {
            "id": "lifetime_throughput",
            "name": "Lifetime Throughput",
            "units": "MWh",
            "value": 29120.43
          }
        ],
        "reports": {
          "types": [
            "executive_summary",
            "cell_temperature",
            "cell_voltage",
          ],
        }
      },
      {
        "id": "betcave",
        "title": "Betcave",
        "onlineRacks": "4/4",
        "status": "Running",
        "upTime": "65%",
        "batteryLevel": "73%",
        "generalMetrics": [
          {
            "id": "net_energy_imported",
            "name": "Net Energy Imported",
            "units": "MWh",
            "value": 896.23
          },
          {
            "id": "net_energy_exported",
            "name": "Net Energy Exported",
            "units": "MWh",
            "value": 841.51
          },
          {
            "id": "net_throughput",
            "name": "Net Throughput",
            "units": "MWh",
            "value": 1735.74
          },
          {
            "id": "lifetime_throughput",
            "name": "Lifetime Throughput",
            "units": "MWh",
            "value": 28120.43
          }
        ],
        "reports": {
          "types": [
            "executive_summary",
            "cell_temperature",
            "cell_voltage",
          ],
        }
      }
    ]
  },
  {
    "client": "SMT",
    "sites": [
      {
        "id": "alvin",
        "title": "Alvin",
        "onlineRacks": "36/36",
        "status": "Running",
        "upTime": "99%",
        "batteryLevel": "75%",
        "generalMetrics": [
          {
            "id": "maximum_humidity",
            "name": "Maximum Humidity",
            "units": "%",
            "value": 1.2
          },
          {
            "id": "minimum_humidity",
            "name": "Minimum Humidity",
            "units": "%",
            "value": 1.2
          }
        ],
        "reports": {
          "types": [
            "executive_summary",
            "cell_temperature",
            "cell_voltage",
          ],
        }
      }
    ]
  }
]


```