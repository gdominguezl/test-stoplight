---
stoplight-id: jpxlhc6k65n71
---

# Endpoint 2 - Get client sites data (Summary) [Variant of endpoint-1]

> **Description:** This endpoint allows users to retrieve summary data for all sites associated with a specific client within a specified date range, while excluding the charts array inside reports. Unlike endpoint-1-get-selected-site-data, which automatically determines the sites based on the user's access permissions, **this endpoint requires the user to specify the client explicitly**.

Query params:
- `client`: Represents the client that owns a group of sites, for example: BRP, NIPSCO, SMT, etc.
- `from`: Represents the start date of the requested summary data. (Format: MM-DD-YYYY)
- `to`: Represents the end date of the requested summary data. (Format: MM-DD-YYYY)
- `summary`: Indicator to get only the general data for the site (excludes charts)

---

**Proposed endpoint:**
```
/sites?client=<clientName>&from=<dateFrom>&to=<dateUntil>&summary=true
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
          "<report_type_1>", // To filter charts by report type.
          "<report_type_2>",
          "<report_type_n>",
        ],
      },
    }
    // ...More sites 
  ]
}

```

**Example:**
Getting summary data for all sites for the BRP client, from=05-01-2023 to 05-02-2023

```
/sites?client=BRP&from=05-01-2023&to=05-02-2023&summary=true
```

**Mocked response (200)**

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
          "events",
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
          "events",
          "poi",
        ],
      }
    }
  ]
}

```