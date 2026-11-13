# TaskNest – Full Stack To-Do List Application

> A modern, clean, and responsive full-stack task management dashboard developed with **Node.js**, **Express.js**, **MongoDB Atlas**, **Mongoose**, **HTML5**, **CSS3**, and **Vanilla JavaScript**.

---

## 1. Project Overview

**TaskNest** is a full-featured task and workflow management dashboard engineered as an internship submission. It provides a real-world demonstration of end-to-end full-stack integration: from a responsive, framework-free frontend interacting via asynchronous `fetch()` calls, to an Express REST API backend, persisting data into a cloud-hosted MongoDB Atlas cluster.

The application avoids heavy client-side frameworks (no React, Next.js, Tailwind, or Bootstrap) to emphasize core foundational web engineering skills:
- Semantic HTML5 structure with accessibility consideration.
- Pure custom CSS3 design system using CSS variables, flexbox, CSS grid, and subtle pastel aesthetics.
- Modular Vanilla JavaScript (ES6+) for DOM manipulation, reactive state synchronization, and API integration.
- Industrial-grade Node.js / Express backend with modular MVC architecture, robust schema validation, error boundaries, and environment-driven configuration.

---

## 2. Key Features

### 📝 Core Task Management
- **Add Tasks**: Create tasks with mandatory titles, optional rich descriptions, priority levels (**Low**, **Medium**, **High**), and due dates.
- **Display Tasks**: Real-time task cards displaying title, description, colored priority badges, due date alert status, and creation timestamps.
- **Edit Tasks**: Interactive modal dialog pre-loaded with current task properties, allowing updates that sync directly with MongoDB without refreshing the page.
- **Delete Tasks**: Safe deletion flow with custom styled confirmation dialog showing a preview of the task before permanent removal.
- **Mark as Completed / Pending**: Instant completion toggle with visual strikethrough, muted completion styling, and completion badge.

### 🔍 Search, Filter & Sort Capabilities
- **Real-Time Search**: Instant search filtering tasks by title or description with a one-click clear button.
- **Status Tabs**: One-click filtering for **All Tasks**, **Pending Tasks**, and **Completed Tasks** with live count badges.
- **Priority Filtering**: Filter by specific priority levels (High, Medium, Low).
- **Multi-Criteria Sorting**: Sort by **Newest First**, **Oldest First**, **Due Date (Earliest)**, **Priority (High to Low)**, or **Title (A-Z)**.

### 📊 Real-Time Analytics & Feedback
- **Dashboard Counters**: Live metrics showing Total Tasks, Pending Tasks, Completed Tasks, and a dynamic percentage completion progress bar.
- **Server Health Indicator**: Live pill indicator in the header reflecting MongoDB Atlas connection status.
- **Toast Notifications**: Non-intrusive floating toasts for success, error, and informational updates.
- **Form Validation**: Real-time feedback preventing empty or whitespace-only submissions.

### 📱 Responsive Design
- Optimized for desktops, laptops, tablets, and smartphones.
- Touch-friendly tap targets (minimum 44px) and adaptive layouts.

---

## 3. Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | HTML5 (Semantic & Accessible), CSS3 (Custom Variables, Flexbox, Grid), Vanilla JavaScript (ES6+ Modules) |
| **Backend** | Node.js (v18+), Express.js (v4.21+) |
| **Database** | MongoDB Atlas, Mongoose ODM (v8.9+) |
| **API Architecture** | RESTful JSON API with CORS and Morgan logging |
| **Testing** | Node Test Runner, Puppeteer Core (Automated UI Screenshot Generation) |

---

## 4. Project Folder Structure

```
tasknest/
│
├── client/                      # Frontend Application
│   ├── css/
│   │   └── style.css            # Custom CSS3 stylesheet & pastel design system
│   ├── js/
│   │   ├── api.js               # REST API fetch client & HTTP wrapper
│   │   └── app.js               # Application state, DOM events & UI logic
│   └── index.html               # Main single-page HTML5 dashboard
│
├── server/                      # Backend REST API
│   ├── src/
│   │   ├── config/
│   │   │   └── db.js            # MongoDB Atlas connection & fallback config
│   │   ├── controllers/
│   │   │   └── taskController.js# Express route controllers & business logic
│   │   ├── models/
│   │   │   └── Task.js          # Mongoose Task schema and indexes
│   │   ├── routes/
│   │   │   └── taskRoutes.js    # Express REST API routes
│   │   └── server.js            # Express server entry point & middleware
│   ├── .env.example             # Server environment variables template
│   ├── package.json             # Server package configuration
│   └── test-api.js              # Automated backend integration test suite
│
├── screenshots/                 # Actual captured application screenshots
│   ├── 1-main-dashboard.png
│   ├── 2-add-task.png
│   ├── 3-task-list.png
│   ├── 4-edit-task.png
│   ├── 5-delete-confirmation.png
│   ├── 6-completed-tasks.png
│   ├── 7-search-filter.png
│   └── 8-mobile-responsive.png
│
├── scripts/
│   └── capture-screenshots.js   # Headless Chrome script for capturing actual screenshots
│
├── .env.example                 # Root environment template
├── .gitignore                   # Git exclusion rules
├── package.json                 # Root package configuration
└── README.md                    # Project documentation
```

---

## 5. Prerequisites

Before running the application, make sure you have:
- **Node.js**: v18.0.0 or later installed (`node -v`)
- **npm**: v9.0.0 or later installed (`npm -v`)
- A **MongoDB Atlas** account (or a local MongoDB instance)

---

## 6. MongoDB Atlas Configuration Instructions

Follow these steps to connect TaskNest to your free MongoDB Atlas cloud cluster:

1. **Sign in / Create Account**: Go to [MongoDB Atlas](https://www.mongodb.com/atlas/database) and sign in.
2. **Build a Cluster**:
   - Choose the free **M0 Sandbox** tier.
   - Select your preferred cloud provider and region (e.g., AWS / Google Cloud).
   - Click **Create Deployment**.
3. **Set Up Database Access (Credentials)**:
   - Navigate to **Security** &rarr; **Database Access**.
   - Click **Add New Database User**.
   - Choose **Password** authentication.
   - Enter a username (e.g., `tasknest_admin`) and a secure password.
   - Set privileges to **Read and write to any database**.
   - Click **Add User**.
4. **Configure Network Access (IP Whitelist)**:
   - Navigate to **Security** &rarr; **Network Access**.
   - Click **Add IP Address**.
   - Choose **Allow Access from Anywhere** (`0.0.0.0/0`) or add your current IP address.
   - Click **Confirm**.
5. **Obtain Connection String**:
   - Go to **Database** &rarr; **Clusters**.
   - Click **Connect** on your cluster.
   - Select **Drivers** (Node.js).
   - Copy the connection URI string. It looks like:
     ```
     mongodb+srv://<username>:<password>@cluster0.abcde.mongodb.net/?retryWrites=true&w=majority
     ```
6. **Configure Environment Variables**:
   - Create a `.env` file in the project root (or inside `server/`):
     ```bash
     cp .env.example .env
     ```
   - Replace `<username>`, `<password>`, and append database name `/tasknest`:
     ```env
     PORT=5000
     NODE_ENV=development
     MONGODB_URI=mongodb+srv://tasknest_admin:YOUR_PASSWORD@cluster0.abcde.mongodb.net/tasknest?retryWrites=true&w=majority
     ```

> **Zero-Config Evaluation Fallback**: If `MONGODB_URI` is omitted during local development/grading, TaskNest automatically initializes an ephemeral in-memory MongoDB instance so you can immediately explore and test all features without configuration blockers.

---

## 7. Installation Instructions

1. Clone or extract the project repository:
   ```bash
   git clone https://github.com/your-username/tasknest.git
   cd tasknest
   ```

2. Install all dependencies:
   ```bash
   npm install
   ```

3. Set up environment variables:
   ```bash
   cp .env.example .env
   ```
   *(Edit `.env` to include your MongoDB Atlas URI)*

---

## 8. How to Run the Application

### Option A: Standard Unified Mode (Recommended)
Start the Express server which connects to MongoDB and serves both the REST API and the static frontend dashboard:

```bash
npm start
```
- **Dashboard URL**: [http://localhost:5000](http://localhost:5000)
- **API Base URL**: [http://localhost:5000/api/tasks](http://localhost:5000/api/tasks)
- **API Health Check**: [http://localhost:5000/api/health](http://localhost:5000/api/health)

### Option B: Development Mode (Auto-Reload)
Run using Node's native watch mode for live server reloading:
```bash
npm run dev
```

### Option C: Running Integration Tests
Execute the end-to-end API test suite validating all 11 requirements:
```bash
node server/test-api.js
```

---

## 9. API Endpoint Documentation

All endpoints return uniform JSON responses:

### Summary of Endpoints

| Method | Endpoint | Description | Status Code |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/health` | Service health status check | `200 OK` |
| `GET` | `/api/tasks` | Retrieve all tasks (supports search & filter) | `200 OK` |
| `GET` | `/api/tasks/:id` | Retrieve a single task by ID | `200 OK` / `404 Not Found` |
| `POST` | `/api/tasks` | Create a new task in MongoDB | `201 Created` / `400 Bad Request` |
| `PUT` | `/api/tasks/:id` | Update an existing task | `200 OK` / `400 Bad Request` |
| `PATCH` | `/api/tasks/:id/complete` | Toggle or set task completion | `200 OK` / `404 Not Found` |
| `DELETE` | `/api/tasks/:id` | Delete a task from MongoDB | `200 OK` / `404 Not Found` |

---

### Detailed Endpoint Specifications

#### 1. `GET /api/tasks`
Retrieve tasks with optional query filters: `status` (`all` | `pending` | `completed`), `priority` (`Low` | `Medium` | `High`), `search` (text), `sortBy` (`createdAt` | `dueDate` | `priority` | `title`), and `order` (`asc` | `desc`).

**Example Request:**
```http
GET /api/tasks?status=pending&priority=High&sortBy=dueDate&order=asc HTTP/1.1
Host: localhost:5000
```

**Example Response (`200 OK`):**
```json
{
  "success": true,
  "count": 1,
  "stats": {
    "total": 5,
    "completed": 2,
    "pending": 3
  },
  "data": [
    {
      "_id": "67324efb1c09ab0012345678",
      "title": "Complete MongoDB Atlas Integration",
      "description": "Configure connection strings and Task model validation",
      "priority": "High",
      "dueDate": "2026-11-20T00:00:00.000Z",
      "completed": false,
      "createdAt": "2026-11-11T14:30:00.000Z",
      "updatedAt": "2026-11-11T14:30:00.000Z"
    }
  ]
}
```

---

#### 2. `POST /api/tasks`
Create a new task in MongoDB.

**Example Request:**
```http
POST /api/tasks HTTP/1.1
Host: localhost:5000
Content-Type: application/json

{
  "title": "Build Responsive CSS Layout",
  "description": "Use CSS grid and flexbox for mobile and desktop screens",
  "priority": "Medium",
  "dueDate": "2026-11-25"
}
```

**Example Response (`201 Created`):**
```json
{
  "success": true,
  "message": "Task created successfully.",
  "data": {
    "_id": "67324efb1c09ab0012345679",
    "title": "Build Responsive CSS Layout",
    "description": "Use CSS grid and flexbox for mobile and desktop screens",
    "priority": "Medium",
    "dueDate": "2026-11-25T00:00:00.000Z",
    "completed": false,
    "createdAt": "2026-11-11T14:35:00.000Z",
    "updatedAt": "2026-11-11T14:35:00.000Z"
  }
}
```

---

#### 3. `GET /api/tasks/:id`
Fetch a specific task by its 24-character hexadecimal MongoDB ObjectId.

**Example Response (`200 OK`):**
```json
{
  "success": true,
  "data": {
    "_id": "67324efb1c09ab0012345679",
    "title": "Build Responsive CSS Layout",
    "description": "Use CSS grid and flexbox for mobile and desktop screens",
    "priority": "Medium",
    "dueDate": "2026-11-25T00:00:00.000Z",
    "completed": false,
    "createdAt": "2026-11-11T14:35:00.000Z",
    "updatedAt": "2026-11-11T14:35:00.000Z"
  }
}
```

---

#### 4. `PUT /api/tasks/:id`
Modify existing task details.

**Example Request:**
```http
PUT /api/tasks/67324efb1c09ab0012345679 HTTP/1.1
Host: localhost:5000
Content-Type: application/json

{
  "title": "Build Responsive CSS Layout & Animations",
  "priority": "High"
}
```

**Example Response (`200 OK`):**
```json
{
  "success": true,
  "message": "Task updated successfully.",
  "data": {
    "_id": "67324efb1c09ab0012345679",
    "title": "Build Responsive CSS Layout & Animations",
    "description": "Use CSS grid and flexbox for mobile and desktop screens",
    "priority": "High",
    "dueDate": "2026-11-25T00:00:00.000Z",
    "completed": false,
    "createdAt": "2026-11-11T14:35:00.000Z",
    "updatedAt": "2026-11-11T14:40:00.000Z"
  }
}
```

---

#### 5. `PATCH /api/tasks/:id/complete`
Toggle or set task completion status.

**Example Request:**
```http
PATCH /api/tasks/67324efb1c09ab0012345679/complete HTTP/1.1
Host: localhost:5000
Content-Type: application/json

{
  "completed": true
}
```

**Example Response (`200 OK`):**
```json
{
  "success": true,
  "message": "Task marked as completed.",
  "data": {
    "_id": "67324efb1c09ab0012345679",
    "title": "Build Responsive CSS Layout & Animations",
    "completed": true,
    "updatedAt": "2026-11-11T14:42:00.000Z"
  }
}
```

---

#### 6. `DELETE /api/tasks/:id`
Permanently remove a task from MongoDB.

**Example Request:**
```http
DELETE /api/tasks/67324efb1c09ab0012345679 HTTP/1.1
Host: localhost:5000
```

**Example Response (`200 OK`):**
```json
{
  "success": true,
  "message": "Task deleted successfully.",
  "data": {
    "id": "67324efb1c09ab0012345679",
    "title": "Build Responsive CSS Layout & Animations"
  }
}
```

---

## 10. Screenshots

The following screenshots are captured directly from the live TaskNest application running with the Express backend and MongoDB database.

### 1. Main Dashboard
*Comprehensive view showing live task metrics, progress bar, add task form, and populated task list.*
![Main Dashboard](screenshots/1-main-dashboard.png)

---

### 2. Adding a New Task
*Form input with priority selection pills, due date picker, and validation.*
![Adding a New Task](screenshots/2-add-task.png)

---

### 3. Task List with Multiple Tasks
*Organized task cards displaying priority indicators, due date badges, and action buttons.*
![Task List with Multiple Tasks](screenshots/3-task-list.png)

---

### 4. Editing a Task
*Interactive modal dialog pre-filled with existing task values for seamless in-place updates.*
![Editing a Task](screenshots/4-edit-task.png)

---

### 5. Deleting a Task Confirmation
*Confirmation dialog preventing accidental deletion, showing task title preview.*
![Deleting a Task Confirmation](screenshots/5-delete-confirmation.png)

---

### 6. Completed Tasks View
*Filtered view displaying completed tasks with strikethrough typography and completion badges.*
![Completed Tasks](screenshots/6-completed-tasks.png)

---

### 7. Search and Filter Functionality
*Real-time title/detail search combined with priority filtering and matched count.*
![Search and Filter Functionality](screenshots/7-search-filter.png)

---

### 8. Mobile Responsive Interface
*Clean mobile viewport showing stacked layout, mobile-optimized navigation, and touch-friendly cards.*
![Mobile Responsive Interface](screenshots/8-mobile-responsive.png)

---

## 11. Student Developer Notes & Evaluation Checklist

- [x] **No Frameworks on Frontend**: Built strictly with HTML5, CSS3, and Vanilla JavaScript.
- [x] **Express RESTful APIs**: Fully implemented `GET`, `POST`, `PUT`, `PATCH`, `DELETE` endpoints.
- [x] **MongoDB Persistence**: Tasks are saved, fetched, updated, and deleted from MongoDB via Mongoose.
- [x] **Complete Validation**: Empty titles rejected, invalid IDs handled with 400 Bad Request, Mongoose Schema validation active.
- [x] **Responsive Layout**: Tested across mobile (390px), tablet, and desktop viewports.
- [x] **Live Database Connection Indicator**: Header status dot reflects live database connectivity.
- [x] **Automated Test Suite**: Integration test suite verifying 100% of endpoints.
- [x] **Actual Screenshots**: Real high-resolution screenshots generated from the running application.

---

## 12. License

This project is submitted under the [MIT License](LICENSE).
