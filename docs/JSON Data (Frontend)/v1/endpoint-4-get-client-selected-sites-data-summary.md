---
stoplight-id: 4pb9fkcwyh0fi
---

# Endpoint 4 - Get client selected sites data (Summary) - [Variant of endpoint-3]

> **Description:** This endpoint retrieves summary data for **specified site IDs** associated with a client, **excluding charts data inside the reports array**.

Query params:
- `client`: Represents the client that owns a group of sites, for example: BRP, NIPSCO, SMT, etc.
- `sitesIds`: Represents an array with the ID of specific sites of a client. Example: Alvin (from the BRP client)
- `from`: Represents the start date of the requested summary data. (Format: MM-DD-YYYY)
- `to`: Represents the end date of the requested summary data. (Format: MM-DD-YYYY)
- `summary`(new param): Indicator to get only the general data for the site (excludes charts)

---

**Proposed endpoint**
```
/sites?client=<clientName>&sitesIds=<site_id>,<site_id>&from=<dateFrom>&to=<dateUntil>&summary=true
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
        }
        // .. Other metrics
      ],
      "reports": {
        "types": [
          "<report_type_1>", // To match with reportType key at charts array
          "<report_type_2>",
          "<report_type_n>",
        ],
      },
    },
    {
      "id": "<site_id_2>",
      "title": "<site_title_2>",
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
        }
        // .. Other metrics
      ],
      "reports": {
        "types": [
          "<report_type_1>", // To match with reportType key at charts array
          "<report_type_2>",
          "<report_type_n>",
        ],
      },
    }
    // ...More sites 
  ]
}

```

---

**Example:**

Getting data for **alvin** and **angleton** sites for the BRP client, from=05-01-2023 to 05-02-2023


```
/sites?client=BRP&sitesIds=alvin,angleton&from=05-01-2023&to=05-02-2023&summary=true
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
    }
  ]
}

```





