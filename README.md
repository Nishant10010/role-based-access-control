# Role-Based Access Control (Admin/User/Moderator)

Build role-based access control with Admin, User, and Moderator roles using Node.js and Express.js

## Objective

Learn how to implement role-based access control (RBAC) in a Node.js and Express application to restrict access to certain routes or actions based on user roles. This task helps you understand how to store and check user roles in JWT tokens, create flexible authorization logic, and secure sensitive parts of your backend API.

## Task Description

Create a Node.js and Express.js backend that supports user authentication with different roles, including Admin, User, and Moderator. Implement a login route that issues JWT tokens containing the user's role in the payload. Create middleware to verify the JWT and extract the user's role. Implement separate protected routes that can only be accessed by specific roles, for example:

- An **Admin-only dashboard route**
- A **Moderator management route**
- A general **User profile route**

Ensure that requests with invalid tokens or insufficient roles are properly denied with clear error messages. Test your system by logging in with different roles and accessing each route to confirm that the role-based restrictions work as expected.

## Documentation Images

![Image 1](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qnt88p4/7.png)

![Image 2](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qnt88p4/8.png)

![Image 3](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qnt88p4/9.png)

![Image 4](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qnt88p4/10.png)

## Getting Started

### Prerequisites

- Node.js installed
- npm or yarn package manager
- Basic understanding of Express.js and JWT

### Installation

```bash
npm install
```

### Running the Application

```bash
npm start
```

## Features

- JWT-based authentication
- Role-based access control (Admin, User, Moderator)
- Protected routes with role validation
- Clear error handling for unauthorized access
- Middleware for token verification and role extraction

## Technologies Used

- Node.js
- Express.js
- JWT (jsonwebtoken)
- JavaScript
