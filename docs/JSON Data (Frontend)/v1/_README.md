---
stoplight-id: 8tmppq1ccrvsp
---

> The `v1` folder contains our proposed JSON structures and suggested endpoints for obtaining the corresponding JSON data. These structures have been designed with frontend optimization in mind, focusing on efficient rendering and visualization. It is important to be aware that the actual data received from the cloud may vary from the information presented in these endpoints. As we learn more and identify opportunities for improvement, we may update and refine these structures.

**Main files and endpoints are:**

1. **Char types in endpoints** (file)
Location: `chart-types-in-endpoints.md`

> **Description:** Outlines the proposed data structures for various chart types that may be returned in API endpoint JSON responses.
> 
2. **Get summary data by user authentication** [endpoint]

Location: `endpoint-1-get-summary-data-by-user-auth.md`

> **Description:** This endpoint retrieves summary data for all sites that the current user has access to. In our proposed frontend, this endpoint may be usefull to populate the main screen (See figma).

![Screen Shot 2023-05-10 at 22.45.12.png](<../../../assets/images/Screen Shot 2023-05-10 at 22.45.12.png>)


3. **Get client selected sites data (All)** [endpoint]

Location: `endpoint-3-get-client-selected-site-data.md`

> **Description:** This endpoint retrieves data for multiple site IDs associated with a client, including reports and charts. This endpoint may be useful to populate the key insights area (See Figma)

![Screen Shot 2023-05-10 at 22.50.18.png](<../../../assets/images/Screen Shot 2023-05-10 at 22.50.18.png>)

4. **Get client site reports (All)** [endpoint]

Location: `endpoint-3-get-client-selected-site-data.md`

> **Description:** This endpoint retrieves the reports data for **one specific site ID associated with a client** and it only concerns about the reports array. This endpoint may be useful to populate key insights full area (See Figma)
> 
![Screen Shot 2023-05-10 at 22.53.32.png](<../../../assets/images/Screen Shot 2023-05-10 at 22.53.32.png>)







