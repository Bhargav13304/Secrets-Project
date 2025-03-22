# Secrets Authentication Project

## Overview
The **Secrets Authentication Project** is a full-stack web application that allows users to securely register, log in, and share secrets anonymously. The project integrates **local authentication** and **Google OAuth 2.0** for seamless sign-in functionality. User credentials are securely stored in a **PostgreSQL** database, with passwords encrypted using **bcrypt**. Sessions are managed using **express-session** to maintain user authentication status.

This project follows best security practices and is structured using the **Model-View-Controller (MVC)** design pattern. The front-end is built with **EJS templating**, while the back-end is powered by **Node.js** and **Express.js**.

## Features
- **User Authentication:** Supports local sign-up/sign-in with hashed passwords and Google OAuth login.
- **Session Management:** Uses **express-session** for persistent user authentication.
- **Secure Password Handling:** **bcrypt** is used to encrypt user passwords before storing them.
- **PostgreSQL Database Integration:** Data is stored and managed using **pg** (PostgreSQL library for Node.js).
- **Google OAuth 2.0 Authentication:** Allows users to log in using their Google account.
- **Secrets Submission & Retrieval:** Users can submit anonymous secrets, which are stored and displayed securely.
- **Error Handling & Security:** Implements best practices to prevent vulnerabilities like SQL injection and XSS attacks.

## Technologies Used
### Backend
- **Node.js** - JavaScript runtime environment
- **Express.js** - Web framework for Node.js
- **PostgreSQL** - Relational database for storing user data
- **pg (node-postgres)** - PostgreSQL client for Node.js
- **bcrypt** - Secure password hashing
- **passport.js** - Authentication middleware
- **passport-local** - Local authentication strategy
- **passport-google-oauth2** - Google OAuth strategy for authentication
- **dotenv** - Secure environment variable management
- **express-session** - Session management

### Frontend
- **EJS (Embedded JavaScript)** - Templating engine for rendering dynamic pages
- **CSS & Bootstrap** - Styling and responsive design

## Project Structure
```
/project-root
│── views/               # EJS templates for front-end UI
│   ├── home.ejs         # Home page
│   ├── login.ejs        # Login page
│   ├── register.ejs     # Registration page
│   ├── secrets.ejs      # Secrets page
│   ├── submit.ejs       # Submit secret page
│── public/              # Static assets (CSS, images, etc.)
│── routes/              # Route handlers (optional modularization)
│── index.js             # Main server file
│── solution.js          # Alternative implementation file
│── queries.sql          # SQL queries for setting up the database
│── .env.example         # Sample environment variable file
│── package.json         # Project dependencies and metadata
│── package-lock.json    # Lock file for dependency versions
│── README.md            # Project documentation
```

## Installation & Setup
### 1. Clone the Repository
```sh
git clone https://github.com/your-username/secrets-auth.git
cd secrets-auth
```

### 2. Install Dependencies
```sh
npm install
```

### 3. Configure Environment Variables
Create a `.env` file in the root directory and add the following:
```sh
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
SESSION_SECRET=your_secret_key
PG_USER=your_postgres_user
PG_HOST=localhost
PG_DATABASE=your_database_name
PG_PASSWORD=your_postgres_password
PG_PORT=5432
```
> **Note:** Never push the `.env` file to GitHub! Use `.gitignore` to exclude it.

### 4. Set Up PostgreSQL Database
Ensure PostgreSQL is installed and running. Create a new database and run the `queries.sql` file:
```sh
psql -U your_postgres_user -d your_database_name -f queries.sql
```

### 5. Start the Server
```sh
npm start
```
The server will be running on `http://localhost:3000/`.

## Google OAuth 2.0 Setup
1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Create a new **OAuth 2.0 Client ID**.
3. Configure the **Authorized Redirect URIs**:
   - `http://localhost:3000/auth/google/secrets`
4. Copy the **Client ID** and **Client Secret** into your `.env` file.
5. Enable the **Google+ API** (for fetching user profiles).

## How the Application Works
### Authentication Flow
1. **User Registration**
   - User registers with email and password.
   - Password is hashed using **bcrypt** before storing in the database.
2. **User Login**
   - Password is verified using **bcrypt**.
   - If correct, a session is created using **express-session**.
3. **Google OAuth Login**
   - Redirects user to Google authentication page.
   - Upon successful login, retrieves user profile and stores it in the database if it doesn’t already exist.
4. **Secret Submission**
   - Authenticated users can submit secrets.
   - Secrets are stored in the **users** table in PostgreSQL.
5. **Displaying Secrets**
   - Authenticated users can see stored secrets.

## Deployment on Google Cloud
1. Set up a **Google Cloud VM instance** with Node.js and PostgreSQL installed.
2. Upload project files manually to the instance.
3. Install dependencies:
   ```sh
   npm install
   ```
4. Set environment variables directly on the VM instance instead of using `.env`:
   ```sh
   export GOOGLE_CLIENT_ID=your_google_client_id
   export GOOGLE_CLIENT_SECRET=your_google_client_secret
   export SESSION_SECRET=your_secret_key
   export PG_USER=your_postgres_user
   export PG_HOST=your_postgres_host
   export PG_DATABASE=your_database_name
   export PG_PASSWORD=your_postgres_password
   export PG_PORT=5432
   ```
5. Start the server:
   ```sh
   npm start
   ```
6. Configure **firewall rules** to allow incoming traffic on **port 3000**.
7. Access the application via your VM’s external IP address.



