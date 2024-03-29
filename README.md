# Flix-Backend Service

## Introduction

Flix-Backend is a comprehensive backend service designed to support a front-end application for browsing, managing, and tracking movies and TV shows. It includes functionalities for user authentication, managing watchlists, and accessing detailed information about various entertainment media.

## Features

- **User Authentication**: Secure registration and login processes with JWT for maintaining sessions.
- **Media Catalog**: Access to a wide range of movies and TV shows, including search functionality and detailed media information.
- **Personal Watchlist**: Users can create and manage a personal watchlist for tracking their favorite movies and TV shows.
- **Trending Content**: Endpoint to fetch trending content based on popularity or other criteria.

## Prerequisites

- **Node.js**: JavaScript runtime needed to run the server.
- **npm**: Node Package Manager, for managing dependencies.
- **MongoDB**: Database where all application data is stored.
- **Docker (Optional)**: For containerizing the application and simplifying deployment processes.

## Setup Instructions

### Step 1: Clone the Repository

```sh
git clone https://github.com/AkshaysProjects/flix-backend
cd flix-backend
```

### Step 2: Environment Configuration

Duplicate `.env.example` to `.env` and configure the environment variables:

- `DATABASE_URL`: MongoDB connection string.
- `JWT_SECRET`: Secret key for JWT token generation and verification.

### Step 3: Install Dependencies

```sh
npm install
```

### Step 4: Running the Server

- **Development Mode**: `npm run dev` (uses `nodemon` for hot reloads)
- **Production Mode**: `npm start`

### Step 5: Docker Setup (Optional)

To containerize the application:

```sh
docker build -t flix-backend .
docker-compose up
```

## Detailed API Endpoints

### User Endpoints

- `POST /user/register`: Register a new user.

  - **Body**: `{ "email": "user@example.com", "password": "password123" }`
  - **Response**: User object with JWT token.

- `POST /user/login`: Authenticate and log in a user.

  - **Body**: `{ "email": "user@example.com", "password": "password123" }`
  - **Response**: User object with JWT token.

- `GET /user/me`: Retrieve details of the currently logged-in user.
  - **Headers**: `Authorization: Bearer <token>`
  - **Response**: User object without sensitive information like password.

### Movie Endpoints

- `GET /movies`: Fetch a list of movies with pagination.

  - **Query Parameters**: `?page=<number>`
  - **Response**: Array of movie objects.

- `GET /movies/search`: Search for movies by title.

  - **Query Parameters**: `?query=<searchTerm>`
  - **Response**: Array of movies matching the search criteria.

- `GET /movies/:id`: Get detailed information about a specific movie.
  - **Path Parameters**: `id` (Movie ID)
  - **Response**: Movie object with detailed information.

### TV Show Endpoints

- `GET /tvshows`: Fetch a list of TV shows with pagination.

  - **Query Parameters**: `?page=<number>`
  - **Response**: Array of TV show objects.

- `GET /tvshows/search`: Search for TV shows by title.

  - **Query Parameters**: `?query=<searchTerm>`
  - **Response**: Array of TV shows matching the search criteria.

- `GET /tvshows/:id`: Get detailed information about a specific TV show.
  - **Path Parameters**: `id` (TV Show ID)
  - **Response**: TV show object with detailed information.

### Watchlist Endpoints

- `GET /watchlist`: Retrieve the current user's watchlist.

  - **Headers**: `Authorization: Bearer <token>`
  - **Response**: Array of items in the user's watchlist.

- `POST /watchlist/:id`: Add a movie or TV show to the watchlist.

  - **Headers**: `Authorization: Bearer <token>`
  - **Path Parameters**: `id` (Movie or TV Show ID)
  - **Response**: Success message or error.

- `DELETE /watchlist/:id`: Remove an item from the watchlist.
  - **Headers**: `Authorization: Bearer <token>`
  - **Path Parameters**: `id` (ID of the item to remove from the watchlist)
  - **Response**: Success message or error.

### Trending Endpoint

- `GET /trending`: Fetch trending movies and TV shows.
  - **Response**: Array of trending movies and TV shows.

## Additional Notes

- Ensure MongoDB is running and accessible through the `DATABASE_URL` specified in the `.env` file.
- When running in Docker, ensure the MongoDB connection string (`DATABASE_URL`) is set to the appropriate container name

set in `docker-compose.yml`.

- All endpoints requiring authentication expect a JWT token to be provided in the `Authorization` header as a Bearer token.
