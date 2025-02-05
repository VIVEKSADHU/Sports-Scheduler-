Sports Scheduler

Sports Session Management App

Description

A web-based application designed to manage sports sessions, enabling users to register, log in, create, and join sessions. The platform supports two types of users: Admins and Players.

Admins: Can create sports, manage sessions, and view reports.

Players: Can join available sessions and track their participation.


The app is built using Node.js, Express, PostgreSQL, bcryptjs for authentication, and EJS for rendering dynamic content.


---

Features

Authentication

User registration, login, and logout with secure authentication.


Admin Dashboard

Manage sports and sessions.

View reports on session popularity.


Player Dashboard

View and join available sessions.


Session Management

Admins can create, delete, and cancel sessions.

Players can join and leave sessions.


Reports

Admins can access insights on session popularity by sport.



---

Technologies Used

Node.js – Backend framework.

Express – Web framework for handling routes and server logic.

bcryptjs – Secure password hashing.

PostgreSQL – Database for storing users, sports, and session data.

EJS – Template engine for rendering dynamic HTML pages.

express-session – Manages user authentication sessions.



---

Installation

Prerequisites

Node.js (>=14.x)

npm (Node package manager)

PostgreSQL (>=12.x)


Setup Instructions

1. Clone the Repository

git clone https://github.com/your-username/sports-session-management-app.git

2. Navigate to the Project Directory

cd sports-session-management-app

3. Install Dependencies

npm install

4. Set Up PostgreSQL

1. Create a PostgreSQL database (e.g., sports_sessions).


2. Update the database connection settings in the ./database.js file.


3. Run the following SQL commands to create tables:



CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  role VARCHAR(50) CHECK (role IN ('admin', 'player')) NOT NULL
);

CREATE TABLE sports (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);

CREATE TABLE sessions (
  id SERIAL PRIMARY KEY,
  sport_id INT REFERENCES sports(id),
  creator_id INT REFERENCES users(id),
  team1 VARCHAR(100),
  team2 VARCHAR(100),
  additional_players INT DEFAULT 0,
  date TIMESTAMP,
  venue VARCHAR(255),
  cancelled BOOLEAN DEFAULT FALSE,
  cancellation_reason TEXT
);

CREATE TABLE session_players (
  session_id INT REFERENCES sessions(id),
  player_id INT REFERENCES users(id),
  PRIMARY KEY (session_id, player_id)
);

5. Start the Server

npm start

The application will run on: http://localhost:3000


---

Application Routes

Public Routes

GET / – Home page

GET /login – Login page

POST /login – Handle login

GET /register – Registration page

POST /register – Handle user registration


Admin Routes

GET /admin-dashboard – Admin panel to manage sessions & sports

POST /create-sport – Create a new sport

POST /delete-session – Delete a session

POST /cancel-session – Cancel a session

GET /reports – View session popularity reports


Player Routes

GET /player-dashboard – View and join available sessions

POST /create-session – Create a new session

POST /join-session – Join a session



---

User Roles & Permissions

Admin

✔ Create and manage sports & sessions
✔ View reports on session popularity
✔ Delete or cancel sessions

Player

✔ Register and log in
✔ Join available sessions
✔ View session details and participant lists


---

Security Considerations

Passwords are securely hashed using bcryptjs.

User sessions are managed using express-session to maintain authentication.



---

Contributing

Contributions are welcome!

1. Fork the repository.


2. Create a feature branch (git checkout -b feature-name).


3. Commit your changes (git commit -m "Add new feature").


4. Push to the branch (git push origin feature-name).


5. Open a pull request.



For major changes, please open an issue first to discuss proposed improvements.


---

License

This project is open-source under the MIT License.

