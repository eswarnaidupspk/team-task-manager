================================================================
        TEAM TASK MANAGER - Full Stack Web Application
================================================================

STUDENT DETAILS
---------------
Name    : Eswar Naidu
GitHub  : eswarnaidupspk

----------------------------------------------------------------

LIVE APPLICATION URL
--------------------
https://team-task-manager-production-ef77.up.railway.app

GITHUB REPOSITORY
-----------------
https://github.com/eswarnaidupspk/team-task-manager

BACKEND API URL
---------------
https://team-task-manager-production-207c.up.railway.app/api/health

----------------------------------------------------------------

PROJECT OVERVIEW
----------------
TeamTask is a full-stack collaborative Team Task Management Web
Application. It allows multiple users to create projects, assign
tasks, and track progress with role-based access control.

----------------------------------------------------------------

TECH STACK
----------
Frontend  : HTML5, CSS3, Vanilla JavaScript
Backend   : Node.js, Express.js
Database  : MongoDB Atlas (Mongoose ODM)
Auth      : JWT (JSON Web Tokens)
Deployment: Railway (Backend + Frontend)
Version   : GitHub

----------------------------------------------------------------

FEATURES IMPLEMENTED
--------------------
1. User Authentication
   - Signup with Name, Email, Password
   - Secure login with JWT tokens
   - Token stored in localStorage
   - Protected routes with middleware

2. Project Management
   - Create projects (creator becomes Admin)
   - Admin can add/remove members by email
   - Admin can update member roles
   - Members can view assigned projects

3. Task Management
   - Create tasks with Title, Description, Due Date, Priority
   - Assign tasks to project members
   - Update status: To Do, In Progress, Done
   - Kanban board view (3 columns)
   - Filter by status and priority

4. Dashboard
   - Total projects and tasks count
   - Tasks by status (visual progress bars)
   - Overdue tasks list
   - Tasks per user breakdown
   - Recent tasks list

5. Role-Based Access Control
   Admin:
   - Create, edit, delete tasks
   - Add/remove project members
   - Change member roles
   - View all project tasks

   Member:
   - View assigned tasks only
   - Update task status only

----------------------------------------------------------------

PROJECT STRUCTURE
-----------------
task-manager/
├── backend/
│   ├── models/
│   │   ├── User.js         (User schema with bcrypt)
│   │   ├── Project.js      (Project + members schema)
│   │   └── Task.js         (Task schema with indexes)
│   ├── routes/
│   │   ├── auth.js         (Signup, Login, Profile)
│   │   ├── projects.js     (CRUD + member management)
│   │   ├── tasks.js        (CRUD with role checks)
│   │   └── dashboard.js    (Stats aggregation)
│   ├── middleware/
│   │   ├── auth.js         (JWT verification)
│   │   └── projectRole.js  (Admin/Member guards)
│   └── server.js           (Express app entry point)
└── frontend/
    ├── index.html          (Single page application)
    ├── styles.css          (Responsive UI styles)
    └── app.js              (All client-side logic)

----------------------------------------------------------------

API ENDPOINTS
-------------
Auth:
  POST   /api/auth/signup         Register new user
  POST   /api/auth/login          Login user
  GET    /api/auth/me             Get current user

Projects:
  GET    /api/projects            Get all user projects
  POST   /api/projects            Create project
  GET    /api/projects/:id        Get project details
  PUT    /api/projects/:id        Update project (Admin)
  DELETE /api/projects/:id        Delete project (Admin)
  POST   /api/projects/:id/members         Add member
  DELETE /api/projects/:id/members/:userId Remove member
  PUT    /api/projects/:id/members/:userId/role  Update role

Tasks:
  GET    /api/tasks/project/:id   Get project tasks
  POST   /api/tasks               Create task (Admin)
  GET    /api/tasks/:id           Get single task
  PUT    /api/tasks/:id           Update task
  DELETE /api/tasks/:id           Delete task (Admin)

Dashboard:
  GET    /api/dashboard           Get overall stats
  GET    /api/dashboard/project/:id  Get project stats

----------------------------------------------------------------

DATABASE DESIGN
---------------
Users Collection:
  - _id, name, email, password (hashed), createdAt

Projects Collection:
  - _id, name, description, createdBy (ref: User)
  - members: [{ user (ref: User), role: Admin|Member }]
  - createdAt, updatedAt

Tasks Collection:
  - _id, title, description, project (ref: Project)
  - assignedTo (ref: User), createdBy (ref: User)
  - status: To Do|In Progress|Done
  - priority: Low|Medium|High
  - dueDate, createdAt, updatedAt

----------------------------------------------------------------

DEPLOYMENT
----------
Platform  : Railway (https://railway.app)
Database  : MongoDB Atlas (Free Tier M0)
Backend   : Node.js service on Railway (us-west-2)
Frontend  : Static site served via Caddy on Railway

Environment Variables used:
  MONGO_URI    - MongoDB Atlas connection string
  JWT_SECRET   - Secret key for JWT signing
  NODE_ENV     - production
  FRONTEND_URL - Frontend URL for CORS

----------------------------------------------------------------

HOW TO RUN LOCALLY
------------------
1. Clone the repository:
   git clone https://github.com/eswarnaidupspk/team-task-manager.git

2. Setup backend:
   cd task-manager/backend
   npm install
   cp .env.example .env
   (Edit .env with your MongoDB URI and JWT secret)
   npm start

3. Open frontend:
   Open task-manager/frontend/index.html in browser
   (Use Live Server in VS Code for best experience)

----------------------------------------------------------------

SECURITY FEATURES
-----------------
- Passwords hashed with bcryptjs (salt rounds: 10)
- JWT tokens expire in 7 days
- Input validation with express-validator
- HTML output escaped to prevent XSS
- CORS restricted to known origins
- .env file excluded from git repository
- Role-based middleware on all protected routes

================================================================
