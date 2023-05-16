---
stoplight-id: 9lbs8g6b8i9wy
---

# Endpoint 3 - Get client selected sites data (All)

> **Description:** This endpoint retrieves data for multiple site IDs associated with a client, including reports and charts. 

Query params:
- `client`: Represents the client that owns a group of sites, for example: BRP, NIPSCO, SMT, etc.
- `sitesIds`: Represents an array with the ID of specific sites of a client. Example: Alvin (from the BRP client)
- `from`: Represents the start date of the requested summary data. (Format: MM-DD-YYYY)
- `to`: Represents the end date of the requested summary data. (Format: MM-DD-YYYY)

---

**Proposed endpoint:**


```
/sites?client=<clientName>&sitesIds=<site_id>,<site_id>&from=<dateFrom>&to=<dateUntil>
```


**Proposed JSON structure**

```json
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
}

```

---

**Example:**

Getting data for alvin and angleton sites for the BRP client, from=05-01-2034 to 05/02/2023

Endpoint:
```
/sites?client=BRP&sitesIds=alvin,angleton&from=05-01-2023&to=05-02-2023
```

JSON Response (200):
```json
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
      ],
      "reports": {
        "types": [
          "executive_summary", // To match with reportType key at charts array
          "cell_temperature", // TODO: Add charts with this report_type
          "cell_voltage", // // TODO: Add charts with this report_type
        ],
        "charts": [
          {
            "chartType": "groupedBar",
            "reportType": "executive_summary",
            "title": "Max/Min Cell Temperature",
            "xAxisTitle": "BESS Number",
            "yAxisTitle": "Temperature (°C)",
            "xAxisLabels": ["BESS1", "BESS2", "BESS3", "BESS4"],
            "yAxisLabels": [0, 20, 30, 40, 50],
            "data": [
              {
                "label": "Maximum",
                "unit": "°C",
                "values": [
                  {
                    "x": "BESS1",
                    "y": 34
                  },
                  {
                    "x": "BESS2",
                    "y": 32
                  },
                  {
                    "x": "BESS3",
                    "y": 33
                  },
                  {
                    "x": "BESS4",
                    "y": 33
                  }
                ]
              },
              {
                "label": "Minimum",
                "unit": "°C",
                "values": [
                  {
                  "x": "BESS1",
                  "y": 21
                  },
                  {
                  "x": "BESS2",
                  "y": 20
                  },
                  {
                  "x": "BESS3",
                  "y": 21
                  },
                  {
                  "x": "BESS4",
                  "y": 21
                  }
                ]
              }
            ]
          },
          {
            "chartType": "groupedBarWithLine",
            "reportType": "executive_summary",
            "title": "Max/Min Cell SOC",
            "xAxisTitle": "BESS Number",
            "yAxisTitle": "State of Charge (%)",
            "xAxisLabels": ["BESS1", "BESS2", "BESS3", "BESS4"],
            "yAxisLabels": [0, 20, 40, 60, 80, 100],
            "data": [
              {
                "label": "Minimum",
                "unit": "%",
                "values": [
                  {
                    "x": "BESS1",
                    "y": 0
                  },
                  {
                    "x": "BESS2",
                    "y": 0
                  },
                  {
                    "x": "BESS3",
                    "y": 0
                  },
                  {
                    "x": "BESS4",
                    "y": 0
                  }
                ]
              },
              {
                "label": "Maximum",
                "unit": "%",
                "values": [
                  {
                    "x": "BESS1",
                    "y": 100
                  },
                  {
                    "x": "BESS2",
                    "y": 100
                  },
                  {
                    "x": "BESS3",
                    "y": 100
                  },
                  {
                    "x": "BESS4",
                    "y": 100
                  }
                ]
              },
              {
                "label": "Average SOC",
                "unit": "%",
                "type": "line",
                "values": [
                  {
                    "x": "BESS1",
                    "y": 63.16962
                  },
                  {
                    "x": "BESS2",
                    "y": 63.16962
                  },
                  {
                    "x": "BESS3",
                    "y": 63.16962
                  },
                  {
                    "x": "BESS4",
                    "y": 63.16962
                  }
                ]
              }
            ]
          },
        ]
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
      ],
      "reports": {
        "types": [
          "executive_summary", // To match with reportType key at charts array
          "cell_temperature", // TODO: Add charts with this type
          "cell_voltage", // TODO: Add charts with this type
        ],
         "charts": [
          {
            "chartType": "groupedBar",
            "reportType": "executive_summary",
            "title": "Max/Min Cell Temperature",
            "xAxisTitle": "BESS Number",
            "yAxisTitle": "Temperature (°C)",
            "xAxisLabels": ["BESS1", "BESS2", "BESS3", "BESS4"],
            "yAxisLabels": [0, 20, 30, 40, 50],
            "data": [
              {
                "label": "Maximum",
                "unit": "°C",
                "values": [
                  {
                    "x": "BESS1",
                    "y": 35
                  },
                  {
                    "x": "BESS2",
                    "y": 31
                  },
                  {
                    "x": "BESS3",
                    "y": 36
                  },
                  {
                    "x": "BESS4",
                    "y": 34
                  }
                ]
              },
              {
                "label": "Minimum",
                "unit": "°C",
                "values": [
                  {
                    "x": "BESS1",
                    "y": 22
                  },
                  {
                    "x": "BESS2",
                    "y": 19
                  },
                  {
                    "x": "BESS3",
                    "y": 23
                  },
                  {
                    "x": "BESS4",
                    "y": 21
                  }
                ]
              }
            ]
          },
          {
            "chartType": "line",
            "reportType": "executive_summary",
            "title": "Daily Meters Net Reading",
            "xAxisTitle": "Date",
            "yAxisTitle": "Energy (MWh)",
            "data": [
              {
                "label": "Throughput",
                "color": "#1f77b4",
                "unit": "MWh",
                "values": [
                  {
                    "x": "2023-03-05",
                    "y": 70.3142
                  },
                  {
                    "x": "2023-03-06",
                    "y": 44.2351
                  },
                  {
                    "x": "2023-03-28",
                    "y": 54.2314
                  },
                  {
                    "x": "2023-03-29",
                    "y": 60.8974
                  }
                ]
              },
              {
                "label": "Energy Imported",
                "color": "#ff7f0e",
                "unit": "MWh",
                "values": [
                  {
                    "x": "2023-03-05",
                    "y": 35.28
                  },
                  {
                    "x": "2023-03-06",
                    "y": 22.87
                  },
                  {
                    "x": "2023-03-28",
                    "y": 28.94
                  },
                  {
                    "x": "2023-03-29",
                    "y": 31.87
                  }
                ]
              },
              {
                "label": "Energy Exported",
                "color": "#2ca02c",
                "unit": "MWh",
                "values": [
                  {
                    "x": "2023-03-05",
                    "y": 35.03
                  },
                  {
                    "x": "2023-03-06",
                    "y": 21.36
                  },
                  {
                    "x": "2023-03-28",
                    "y": 25.29
                  },
                  {
                    "x": "2023-03-29",
                    "y": 29.02
                  }
                ]
              }
             ]
          }
        ]
      }
    }
  ]
}

```




