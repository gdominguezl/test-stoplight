---
stoplight-id: 0oy1i5hh9s2ax
---

# New User Authentication

> Description: This document outlines the new proposed authentication process for the Analyze App, where we systematically outline the user roles, invitation flows and a database structure aimed at ensuring optimal scalability.

## **User Invitation diagram**

In the following diagram, we outline the user invitation flow in our application, detailing the capalities of each user role, this roles are: **Super Admin**, **Harmony**, **Internal User** and **Client User**.

![Screen Shot 2023-05-15 at 13.05.35.png](<../../assets/images/Screen Shot 2023-05-15 at 13.05.35.png>)

In this flow:

- **Super Admin**: The Super Admin has the highest level of access and is capable of creating and sending invitations via email to:
  - New Harmony users, allowing them to log into the app.
  - New Internal Users, granting them access to the app.
  - Additional Super Admins, extending administrative access to others.

- **Harmony**: Harmony users hold the ability to create and send invitations to new Client Users. These invitations are specific to the Harmony user's own organization, thus maintaining organization-specific access control.

- **Internal User**: The Internal User role is designed to receive invitations, rather than send them. An Internal User can receive invitations to join one or multiple organizations, expanding their access within the app as needed.

- **Client User**: Similar to the Internal User, the Client User role is intended to receive invitations. However, a Client User is restricted to joining a single organization, ensuring focused access to specific organization resources.

In this structure, user roles are clearly delineated, providing a level of access control and invitation capability tailored to each role's requirements. This allows for efficient and organized user management within the application.

## Database Structure

It involves five main tables: **Users**, **UserRoles**, **UserOrganization**, **Organizations** and **Invitations**:

Each table serves a unique purpose and collectively they provide a flexible and scalable structure for managing users, their roles, and their organization affiliations.

The **Users** table stores individual user information, while the **UserRoles** table stores possible roles a user can have. The role_id in the Users table corresponds to the id in the UserRoles table (foreign key), defining the role of each user.

The **Organizations** table stores information about each organization. The **UserOrganization** table maps users to organizations, allowing for a many-to-many relationship where a user can belong to multiple organizations and an organization can have multiple users.

The **Invitations** table, will keep track of the tokens created for each invitation, as well as which user created the invitation and for which role and organization it was intended. Also we will be able to control the limit use of each token to one time only or to set an expiration date for those invitations.

### Users

- `id` (number): A unique identifier for each user.
- `username` (string): The username of the user.
- `email` (string): The user's email address.
- `role_id` (number): The id of the user's role.

### UserRoles

- `id` (number): A unique identifier for each role.
- `name` (string): The name of the role.

### Organizations

- `id` (number): A unique identifier for each organization.
- `name` (string): The name of the organization.

### UserOrganization

- `user_id` (number): The id of the user.
- `organization_id` (number): The id of the organization.

### Invitations

- `id` (number): A unique identifier for each invitation.
- `token` (string): The unique token generated for the invitation.
- `created_by` (number): The id of the user who created the invitation.
- `role_id` (number): The id of the role intended for the invited user.
- `organization_id` (number): The id of the organization the invitation is linked to.
- `used` (boolean): A flag to indicate whether the invitation has been used.
- `expires_at` (datetime): The expiration date and time for the invitation.

### Suggested Libraries/Technologies to start:

For implementing the above database structure in a NestJS backend, we can use the following libraries:

- **TypeORM**: This is a powerful ORM (Object Relational Mapper) that can be used with TypeScript, which NestJS is built with. It supports a wide range of databases including PostgreSQL, MySQL, and SQLite.

- **Passport**: This is a popular authentication middleware for Node.js. Passport's comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more. It can be integrated with NestJS using @nestjs/passport module where we can use 'passport-azure-ad' strategy for Microsoft SSO.

- **JWT (JSON Web Tokens)**: JWT is a compact, URL-safe means of representing claims to be transferred between two parties. It's commonly used for Bearer tokens in OAuth 2.0.

- **class-validator and class-transformer**: These libraries are useful for validating and transforming request payloads.

- **Moment.js or date-fns**, for handling the expires_at field in the Invitations table.
