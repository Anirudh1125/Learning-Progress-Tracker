# Learning Progress Tracker

A full-stack web application for tracking learning goals and progress with milestone management.

## Live Deployment

- **Frontend:** https://frontend-learning-progress-tracker.vercel.app/
- **Backend API:** https://backend-learning-progress-tracker.onrender.com
- **Video Demo:** https://drive.google.com/file/d/1fUhvnsxtIvaOUgdaUjfbmWpkBc1yfIjn/view?usp=sharing

## Features

- User authentication with Google OAuth 2.0
- Create, read, update, and delete learning goals
- Milestone tracking with progress calculation
- Interactive dashboard with charts and statistics
- Real-time progress visualization
- Search and filter functionality
- Responsive design for mobile and desktop
- Persistent sessions across page refreshes

## Technology Stack

### Frontend
- React 18 with TypeScript
- React Router for navigation
- Context API with useReducer for state management
- Recharts for data visualization
- Lucide React for icons
- Axios for HTTP requests
- Google OAuth integration
- Deployed on Vercel

### Backend
- Node.js with Express
- MongoDB with Mongoose ODM
- JWT for authentication
- Google OAuth verification
- CORS enabled
- Input validation with Express Validator
- Deployed on Render

## Prerequisites

- Node.js v18 or higher
- npm v9 or higher
- MongoDB Atlas account (or local MongoDB)
- Google Cloud Platform account for OAuth credentials
- Git

## Setup Instructions

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd learning-progress-tracker
```

### 2. Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file in the backend directory:

```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/learning_tracker
GOOGLE_CLIENT_ID=your_google_client_id.apps.googleusercontent.com
JWT_SECRET=your_random_secret_key_here
PORT=5000
FRONTEND_URL=http://localhost:5173
NODE_ENV=development
```

### 3. Frontend Setup

```bash
cd frontend/Learning_prog_tracker
npm install
```

Create a `.env` file in the frontend directory:

```env
VITE_API_URL=http://localhost:5000/api
VITE_GOOGLE_CLIENT_ID=your_google_client_id.apps.googleusercontent.com
```

### 4. Google OAuth Configuration

1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project or select existing
3. Navigate to "APIs & Services" > "Credentials"
4. Create OAuth 2.0 Client ID
5. Application type: Web application
6. Add authorized JavaScript origins:
   - `http://localhost:5173`
   - `http://localhost:5000`
7. Add authorized redirect URIs (same as origins)
8. Copy the Client ID to both `.env` files

### 5. MongoDB Atlas Setup

1. Create account at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new cluster (free tier)
3. Create a database user
4. Whitelist your IP address (or use `0.0.0.0/0` for development)
5. Get connection string and add to `MONGODB_URI` in backend `.env`

## Running the Application

### Start Backend

```bash
cd backend
npm start
```

Backend will run on `http://localhost:5000`

### Start Frontend

```bash
cd frontend/Learning_prog_tracker
npm run dev
```

Frontend will run on `http://localhost:5173`

### Access the Application

Open your browser and navigate to `http://localhost:5173`

## Running Tests

The application uses Playwright for end-to-end testing.

### Setup Playwright

```bash
cd frontend/Learning_prog_tracker
npm install -D @playwright/test
npx playwright install
```

### Run Tests

```bash
# Run all tests
npm test

# Run tests in UI mode (interactive)
npm run test:ui

# Run tests in headed mode (watch browser)
npm run test:headed

# View test report
npm run test:report
```

### Test Files

- **Location:** `frontend/Learning_prog_tracker/tests/app.spec.ts`
- **Test Coverage:**
  - Authentication flow
  - Navigation between pages
  - Dashboard functionality
  - Goals CRUD operations
  - Create Goal multi-step form
  - Search and filter features
  - User profile and logout
  - Protected routes
  - Loading states

The test suite includes 14 comprehensive tests covering all major functionality.

## Dev Container

The project includes a Dev Container configuration for consistent development environments.

### Prerequisites

1. Install [Docker Desktop](https://www.docker.com/products/docker-desktop)
2. Install [VS Code](https://code.visualstudio.com/)
3. Install "Dev Containers" extension in VS Code

### Using Dev Container

1. Open project in VS Code
2. Press `F1` → "Dev Containers: Reopen in Container"
3. Wait for container to build (5-10 minutes first time)
4. Install dependencies:
   ```bash
   cd backend && npm install
   cd ../frontend/Learning_prog_tracker && npm install
   ```

The Dev Container provides:
- Node.js 18 runtime
- Pre-configured VS Code extensions
- Port forwarding (5173, 5000)
- Isolated development environment

## Project Structure

```
learning-progress-tracker/
├── .devcontainer/              # Dev Container configuration
│   └── devcontainer.json
├── backend/                    # Express backend
│   ├── models/                 # MongoDB schemas
│   │   ├── User.js
│   │   └── Goal.js
│   ├── routes/                 # API endpoints
│   │   ├── auth.js
│   │   ├── goals.js
│   │   └── courses.js
│   ├── middleware/             # Authentication middleware
│   │   └── auth.js
│   ├── server.js               # Express application
│   ├── Dockerfile              # Docker configuration
│   ├── .dockerignore
│   ├── .gitignore
│   ├── .env
│   └── package.json
├── frontend/Learning_prog_tracker/  # React frontend
│   ├── src/
│   │   ├── components/         # Reusable components
│   │   │   └── Navbar.tsx
│   │   ├── pages/              # Page components
│   │   │   ├── Dashboard.tsx
│   │   │   ├── Goals.tsx
│   │   │   ├── GoalDetail.tsx
│   │   │   ├── CreateGoal.tsx
│   │   │   ├── Courses.tsx
│   │   │   └── Login.tsx
│   │   ├── context/            # State management
│   │   │   ├── AuthContext.tsx
│   │   │   └── GoalContext.tsx
│   │   ├── utils/              # Helper functions
│   │   │   └── api.ts
│   │   ├── styles/             # CSS files
│   │   ├── App.tsx
│   │   └── main.tsx
│   ├── tests/                  # Playwright tests
│   │   └── app.spec.ts
│   ├── playwright.config.ts
│   ├── .env
│   ├── .gitignore
│   └── package.json
├── ARCHITECTURE.md             # Architecture documentation
├── DEPLOYMENT.md               # Deployment guide
├── TESTING.md                  # Testing documentation
└── README.md                   # This file
```

## Design Artifact

### Sequence Diagram: User Authentication Flow

```
User                    Frontend                 Backend                  Google OAuth             MongoDB
 |                         |                        |                          |                       |
 |--Click "Sign in"------->|                        |                          |                       |
 |                         |                        |                          |                       |
 |                         |--Open Google popup---->|                          |                       |
 |                         |                        |                          |                       |
 |<----Authorize app----------------------------- -->|                          |                       |
 |                         |                        |                          |                       |
 |                         |<--Return credential----|                          |                       |
 |                         |                        |                          |                       |
 |                         |--POST /api/auth/google->|                          |                       |
 |                         |   (with credential)    |                          |                       |
 |                         |                        |                          |                       |
 |                         |                        |--Verify token----------->|                       |
 |                         |                        |                          |                       |
 |                         |                        |<--User info--------------|                       |
 |                         |                        |                          |                       |
 |                         |                        |--Find/Create user----------------------->|       |
 |                         |                        |                          |              |       |
 |                         |                        |<--User document--------------------------        |
 |                         |                        |                          |                       |
 |                         |                        |--Generate JWT            |                       |
 |                         |                        |                          |                       |
 |                         |<--Return JWT + user----|                          |                       |
 |                         |                        |                          |                       |
 |--Store in localStorage--|                        |                          |                       |
 |                         |                        |                          |                       |
 |--Navigate to Dashboard->|                        |                          |                       |
 |                         |                        |                          |                       |
 |                         |--GET /api/goals------->|                          |                       |
 |                         |   (with JWT header)    |                          |                       |
 |                         |                        |                          |                       |
 |                         |                        |--Verify JWT              |                       |
 |                         |                        |                          |                       |
 |                         |                        |--Query goals-------------------------->|         |
 |                         |                        |                          |            |         |
 |                         |                        |<--User's goals----------------------------       |
 |                         |                        |                          |                       |
 |                         |<--Return goals---------|                          |                       |
 |                         |                        |                          |                       |
 |<--Display dashboard-----|                        |                          |                       |
```

### Design Patterns Used

#### 1. Context Provider Pattern
Global state management for authentication and goals using React Context API with useReducer.

**Implementation:**
- `AuthContext`: Manages user authentication state
- `GoalContext`: Manages goals and milestones
- Provides centralized state accessible throughout component tree

#### 2. Reducer Pattern
Predictable state updates through action dispatching.

**Actions:**
- `LOGIN_START`, `LOGIN_SUCCESS`, `LOGIN_FAILURE`
- `SET_GOALS`, `ADD_GOAL`, `UPDATE_GOAL`, `DELETE_GOAL`
- `SET_CURRENT_GOAL`, `SET_LOADING`, `SET_ERROR`

#### 3. Higher-Order Component (HOC) Pattern
`ProtectedRoute` component wraps routes requiring authentication.

**Implementation:**
```typescript
const ProtectedRoute = ({ children }) => {
  return isAuthenticated ? children : <Navigate to="/login" />;
};
```

#### 4. Custom Hooks Pattern
Reusable logic extraction (can be extended for API calls, form handling).

#### 5. Singleton Pattern
API client (axios instance) created once and reused throughout the application.

## API Documentation

### Authentication

#### POST /api/auth/google
Authenticate with Google OAuth token.

**Request:**
```json
{
  "credential": "google_oauth_token"
}
```

**Response:**
```json
{
  "token": "jwt_token",
  "user": {
    "id": "user_id",
    "email": "user@example.com",
    "name": "User Name",
    "picture": "profile_picture_url"
  }
}
```

### Goals

#### GET /api/goals
Get all goals for authenticated user.

**Headers:** `Authorization: Bearer <jwt_token>`

**Response:**
```json
[
  {
    "_id": "goal_id",
    "title": "Learn React",
    "description": "Master React fundamentals",
    "category": "Programming",
    "status": "in-progress",
    "targetDate": "2025-12-31",
    "milestones": [...],
    "userId": "user_id",
    "createdAt": "2025-01-01T00:00:00.000Z"
  }
]
```

#### POST /api/goals
Create a new goal.

#### GET /api/goals/:id
Get a specific goal.

#### PUT /api/goals/:id
Update a goal.

#### DELETE /api/goals/:id
Delete a goal.

#### PUT /api/goals/:id/milestones/:milestoneId/toggle
Toggle milestone completion status.

## Deployment

The application is deployed using:
- **Frontend:** Vercel (automatic deployments from GitHub)
- **Backend:** Render (containerized deployment)
- **Database:** MongoDB Atlas (cloud database)

See [Setup.md](Setup.md) for detailed instructions.

## External Sources & Attribution

### Frontend Libraries
- [React](https://react.dev/) - UI framework
- [React Router](https://reactrouter.com/) - Routing
- [Recharts](https://recharts.org/) - Charts
- [Lucide React](https://lucide.dev/) - Icons
- [Axios](https://axios-http.com/) - HTTP client
- [@react-oauth/google](https://www.npmjs.com/package/@react-oauth/google) - Google OAuth

### Backend Libraries
- [Express](https://expressjs.com/) - Web framework
- [Mongoose](https://mongoosejs.com/) - MongoDB ODM
- [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) - JWT auth
- [google-auth-library](https://www.npmjs.com/package/google-auth-library) - Google OAuth
- [express-validator](https://express-validator.github.io/) - Input validation

### Documentation & Learning Resources
- [MongoDB Atlas Documentation](https://www.mongodb.com/docs/atlas/)
- [Google OAuth 2.0 Documentation](https://developers.google.com/identity/protocols/oauth2)
- [JWT Introduction](https://jwt.io/introduction)
- [React TypeScript Cheatsheet](https://react-typescript-cheatsheet.netlify.app/)
- [Express Security Best Practices](https://expressjs.com/en/advanced/best-practice-security.html)
- [Playwright Documentation](https://playwright.dev/)

## Known Issues

- Goals list requires manual refresh after deletion (trade-off to prevent infinite render loops)
- Render free tier: Backend sleeps after 15 minutes of inactivity (first request may be slow)

## Future Enhancements

- Real-time goal updates with WebSocket
- Course recommendations based on goals
- Goal sharing and collaboration features
- Notifications for approaching deadlines
- Progress reports export (PDF/CSV)
- Mobile application
- Dark mode support
- Achievement badges and gamification

## Author

Anirudh - Learning Program Tracker

## Acknowledgments

- Google Cloud Platform for OAuth services
- MongoDB Atlas for database hosting
- Vercel and Render for deployment platforms