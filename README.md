
# Coy Discover — SDE Intern Assignment (Part B)

A mobile-first, standalone **React + Express** swipe application demonstrating a privacy-first mutual matching experience.

Built as part of the **Coy SDE Intern Assignment**.

This is an unofficial assignment demo, not Coy's actual application.

## Project Overview

Coy Discover is a swipe-based discovery application inspired by Tinder and Bumble.

Users can browse profiles, swipe right to like or left to pass, and view matches when two users like each other.

The application follows Coy's core privacy principle: **Never reveal who has liked the user unless the interest is mutual.**

## Tech Stack

**Frontend**
- React.js
- Vite
- CSS3
- JavaScript

**Backend**
- Node.js
- Express.js
- REST APIs

**Database**
- Local JSON file for persistent storage

**Development Tools**
- Visual Studio Code
- npm
- Postman
- Git and GitHub

## Features

- Home and Discover tabs
- Blank Home tab as required
- 30 fictional mock profiles
- Profile photos, ages, bios, locations, and interests
- Swipe right to like
- Swipe left to pass
- Mobile drag gestures
- Desktop Like and Pass buttons
- Smooth card animations
- Mutual matching system
- "It's a match!" notification
- Matches view
- Privacy protection for incoming likes
- Swipe history persistence
- Match persistence across page reloads
- Prevention of duplicate swipes
- Empty state when all profiles have been viewed
- Backend API testing

## Project Structure

```text
coy-discover/
│
├── frontend/
│   ├── public/
│   │   └── avatars/
│   ├── src/
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   ├── api.js
│   │   └── styles.css
│   ├── package.json
│   └── vite.config.js
│
├── backend/
│   ├── src/
│   │   ├── domain.js
│   │   ├── seed.js
│   │   └── storage.js
│   ├── scripts/
│   │   └── reset.js
│   ├── test/
│   │   └── domain.test.js
│   ├── server.js
│   └── package.json
│
├── Coy_Discover_Postman_Collection.json
└── README.md
```

## Installation and Setup

### Prerequisites

Before running the project, install:

- Node.js 20 or higher
- npm
- Visual Studio Code

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/coy-discover.git
cd coy-discover
```

Replace `YOUR_USERNAME` with your GitHub username.

If you downloaded the project as a ZIP file, extract it and open the `coy-discover` folder in VS Code.

### 2. Install Backend Dependencies

Open a terminal and run:

```bash
cd backend
npm install
```

### 3. Start the Backend Server

```bash
npm run dev
```

The backend server runs at:

```text
http://localhost:4000
```

### 4. Install Frontend Dependencies

Open another terminal from the main project folder.

```bash
cd frontend
npm install
```

If npm reports a peer-dependency conflict, try:

```bash
npm install --legacy-peer-deps
```

### 5. Start the Frontend

```bash
npm run dev
```

Open your browser and visit:

```text
http://localhost:5173
```

Make sure both the frontend and backend servers are running.

## How to Use the Application

1. Open the application in your browser.
2. Navigate to the Discover tab.
3. View the displayed profile.
4. Swipe right or click Like if interested.
5. Swipe left or click Pass if not interested.
6. If both users have liked each other, an "It's a match!" notification appears.
7. Open the Matches view to see mutual matches.
8. Refresh the page to verify that previous swipes and matches are saved.

Some mock profiles are already configured to have liked the logged-in user so that matching can be demonstrated.

## Backend API Endpoints

The backend provides three main REST APIs.

### 1. GET /feed

Returns profiles the user has not already swiped on.

**Request:**

```http
GET http://localhost:4000/feed
```

**Functionality:**
- Returns available profiles
- Excludes previously swiped profiles
- Does not reveal incoming likes

### 2. POST /swipe

Records whether the user likes or passes a profile.

**Request:**

```http
POST http://localhost:4000/swipe
```

**Example Request Body:**

```json
{
  "profileId": 1,
  "action": "like"
}
```

**Example Response Without a Match:**

```json
{
  "matched": false
}
```

**Example Response When a Match Occurs:**

```json
{
  "matched": true,
  "match": {
    "id": 1,
    "name": "Aanya",
    "age": 22,
    "photo": "/avatars/1.svg",
    "bio": "Collecting little moments, sunset walks, and books with bent corners.",
    "location": "Delhi University",
    "interests": [
      "Books",
      "Coffee",
      "Travel"
    ]
  }
}
```

A duplicate swipe is rejected with HTTP status 409.

### 3. GET /matches

Returns the user's mutual matches.

**Request:**

```http
GET http://localhost:4000/matches
```

**Functionality:**
- Returns only mutual matches
- Protects non-mutual incoming likes
- Uses stored swipe information

## Matching Logic

The matching system follows these rules:

1. A user views a profile.
2. The user chooses Like or Pass.
3. The backend records the action.
4. If the user chooses Like, the backend checks whether the other profile has already liked the user.
5. If both users have liked each other, a match is created.
6. The application displays an "It's a match!" notification.
7. Mutual matches appear in the Matches view.

A match is created only when both users have liked each other.

## Privacy and Security

Privacy is a core requirement of this application.

The following measures are implemented:

- Incoming likes remain private.
- Only mutual matches are revealed.
- Previously swiped profiles are excluded from the feed.
- Duplicate swipes are rejected.
- Swipe data is stored on the backend.
- Internal incoming-like information is not exposed in public API responses.

For this assignment, authentication is not required because the application assumes a single logged-in user.

## Data Persistence

The application uses local JSON storage.

- Profile data is seeded automatically.
- Swipe actions are saved.
- Matches remain available after refreshing the page.
- Previously swiped profiles do not reappear.
- Data persists across backend restarts.

## Testing

### Backend Automated Tests

Navigate to the backend folder:

```bash
cd backend
npm test
```

Tests cover:

- Profile data validation
- Feed filtering
- Swipe recording
- Mutual matching
- Privacy protection
- Duplicate swipe prevention
- Data persistence
- Backend API behavior

### Postman Testing

The project includes:

```text
Coy_Discover_Postman_Collection.json
```

To test the APIs:

1. Open Postman.
2. Click Import.
3. Select the collection file.
4. Start the backend server.
5. Test GET `/feed`.
6. Test POST `/swipe`.
7. Test GET `/matches`.

The default API base URL is:

```text
http://localhost:4000
```

## Reset Demo Data

To reset profiles, swipes and matches, navigate to the backend folder and run:

```bash
npm run reset
```

Refresh the frontend afterward.

This restores the initial demo state.

## Future Improvements

Possible future enhancements include:

- User authentication
- Real user profiles
- Profile photo uploads
- Advanced matching preferences
- Real-time chat after matching
- Push notifications
- Profile verification
- Block and report functionality
- Database integration with PostgreSQL or MySQL
- Deployment to a cloud hosting platform

## GitHub Submission

To upload the project to GitHub:

```bash
git init
git add .
git commit -m "Build Coy Discover SDE Intern Assignment"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/coy-discover.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username.

Make sure the repository is public.

Do not upload `node_modules`, generated build files or private environment files.

## Assignment Requirements Covered

| Requirement | Implementation |
|---|---|
| 30 mock profiles | Included |
| Swipe left/right | Included |
| Mobile gestures | Included |
| Desktop buttons | Included |
| Smooth animations | Included |
| Persistent swipes | Included |
| Mutual matching | Included |
| Match notification | Included |
| Matches view | Included |
| Incoming-like privacy | Included |
| GET /feed | Included |
| POST /swipe | Included |
| GET /matches | Included |
| Empty state | Included |
| Automated backend tests | Included |

## Conclusion

Coy Discover is a privacy-focused swipe-based discovery application developed using React.js and Node.js.

The project demonstrates frontend development, REST API design, backend matching logic, persistent data storage, user privacy and responsive UI design.

It fulfills the core technical requirements of Part B of the Coy SDE Intern Assignment.

---

**Project:** Coy Discover

**Assignment:** SDE Intern Assignment — Part B

**Status:** Local development demo

**Repository:** Add your public GitHub repository URL here.
