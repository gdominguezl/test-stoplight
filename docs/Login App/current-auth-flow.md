---
stoplight-id: o7lful9ktn0hm
---

# Current User Authentication Flow

> Description: This document outlines the existing login authentication process for the Dash App. The system utilizes a SQL (SQLite) database to store user information.

### Database Structure

The user information is stored with the following fields:

- `id`: A unique identifier for each user (integer).
- `username`: The username chosen by the user (string).
- `email`: The user's email address (string).
- `approved`: A flag indicating whether the user's account has been approved by an admin (boolean).
- `organization`: A code representing the organization or role of the user (integer).
- `sso_authorized`: A flag indicating whether the user has been authorized for single sign-on (boolean).

### Example Database Entry

| id | username | email                    | approved | organization | sso_authorized |
|----|----------|--------------------------|----------|--------------|----------------|
| 1  | john.doe | john.doe@flexgen.com     | 1        | 100          | 1              |
| 2  | jsmith   | jsmith@example.com       | 0        | 1            | 0              |

### Organization Codes

The `organization` field represents the user's organization or role, and it's defined as follows:

```json
0 = Default (No access)
1 = FlexGen internal user
5 = NPSCO Customer
6 = BRP Customer
7 = NCEMC Customer
8 = SMT Customer
100 = Admin user
```

### User Types

Users can be classified into three types based on their `organization` code:

```json
1. admin (org code 100) 
2. fg_internal_user (org code 1)
3. client_user (org codes 5, 6, 7, 8)
```

The `admin` user is responsible for approving other users and assigning their organization codes. The `fg_internal_user` and `client_user` types are assigned and approved by an `admin` user.

## User Roles and Authentication Flow Diagram

![Screen Shot 2023-05-12 at 13.37.43.png](<../../assets/images/Screen Shot 2023-05-12 at 13.37.43.png>)

In this flow:

1. A new user registers, creating a new user entry in the database with their `username`, `email`, and initial `approved` and `sso_authorized` values set to 0.
2. An `admin` user reviews the new user entry. If the user is approved, the `admin` sets the `approved` value to 1.
3. The `admin` assigns an organization code to the user, which also determines the user's type (`fg_internal_user` or `client_user`).
4. After approval and organization assignment, the user can log into the app.
