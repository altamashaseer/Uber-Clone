# MERN Stack Uber Clone

A full-stack ride-sharing application inspired by Uber, built with the MERN stack (MongoDB, Express, React, Node.js). This project features real-time ride booking and location tracking, separate portals for users and captains (drivers), and integration with the Google Maps API.

This repository is structured as a monorepo with two main directories: `frontend` and `backend`.

## Features

### User Features

- **Authentication**: Secure user registration and login using JSON Web Tokens (JWT).
- **Ride Booking**: Request a ride by specifying pickup and destination addresses.
- **Fare Estimation**: Get an estimated fare for different vehicle types before booking.
- **Real-time Ride Tracking**: See the ride status update in real-time (Confirmed, Started, Ended).
- **Address Autocomplete**: Google Maps-powered address suggestions for easy input.

### Captain (Driver) Features

- **Authentication**: Secure captain registration and login.
- **Vehicle Management**: Register vehicle details (color, plate, capacity, type).
- **Receive Ride Requests**: Get notified of new ride requests from nearby users in real-time.
- **Ride Management**: Accept, start (with OTP verification), and end rides.
- **Real-time Location Updates**: Broadcast current location to the system.

### Core Technical Features

- **Real-time Communication**: Uses **Socket.IO** for instant communication between users, captains, and the server.
- **Geolocation Services**: Integrates with the **Google Maps API** for geocoding, distance calculation, and place suggestions.
- **RESTful API**: A well-structured backend API for handling all application logic.
- **Protected Routes**: Frontend routes are protected to ensure only authenticated users/captains can access specific pages.

## Tech Stack

| Category      | Technology                                                              |
|---------------|-------------------------------------------------------------------------|
| **Frontend**  | React, React Router, Axios, Tailwind CSS, Socket.io-client              |
| **Backend**   | Node.js, Express.js, MongoDB (with Mongoose), Socket.io                 |
| **Auth**      | JSON Web Tokens (JWT)                                                   |
| **APIs**      | Google Maps API (Geocoding, Distance Matrix, Places Autocomplete)       |
| **Database**  | MongoDB (with Mongoose ODM)                                             |

## Getting Started

Follow these instructions to get a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

- Node.js (v18 or later)
- npm
- MongoDB (local instance or a cloud service like MongoDB Atlas)

### Backend Setup

1.  **Navigate to the backend directory:**
    ```sh
    cd Backend
    ```

2.  **Install dependencies:**
    ```sh
    npm install
    ```

3.  **Create an environment file:**
    Create a `.env` file in the `Backend` directory by copying the example file.
    ```sh
    cp .env.example .env
    ```

4.  **Update the environment variables** in `Backend/.env` with your own keys and connection strings:
    - `MONGO_URI`: Your MongoDB connection string.
    - `JWT_SECRET`: A secret key for signing JWTs.
    - `GOOGLE_MAPS_API`: Your Google Maps API key.

5.  **Start the backend server:**
    ```sh
    npm start
    ```
    The server will be running on `http://localhost:3000` (or the port you specify in `.env`).

### Frontend Setup

1.  **Navigate to the frontend directory:**
    ```sh
    cd frontend
    ```

2.  **Install dependencies:**
    ```sh
    npm install
    ```

3.  **Create an environment file:**
    Create a `.env` file in the `frontend` directory by copying the example file.
    ```sh
    cp .env.example .env
    ```

4.  **Update the environment variables** in `frontend/.env` to point to your backend server:
    - `VITE_BASE_URL`: The URL of your running backend (e.g., `http://localhost:3000`).

5.  **Start the frontend development server:**
    ```sh
    npm run dev
    ```
    The application will be available at `http://localhost:5173` (or another port if 5173 is busy).

## API Documentation

The backend provides a complete REST API for all operations. For detailed information on endpoints, request bodies, and example responses, please see the Backend API Documentation.

## Socket.IO Events

Real-time functionality is handled via WebSockets. Here are the key events:

### Client to Server

| Event                     | Payload                            | Description                                      |
|---------------------------|------------------------------------|--------------------------------------------------|
| `join`                    | `{ userId, userType }`             | Associates a user/captain's ID with their socket ID. |
| `update-location-captain` | `{ userId, location: {ltd, lng} }` | Updates the captain's current location.          |

### Server to Client

| Event            | Payload    | Description                                                     |
|------------------|------------|-----------------------------------------------------------------|
| `new-ride`       | `ride`     | Notifies available captains of a new ride request.              |
| `ride-confirmed` | `ride`     | Notifies the user that a captain has accepted their ride.       |
| `ride-started`   | `ride`     | Notifies the user that the ride has officially started.         |
| `ride-ended`     | `ride`     | Notifies the user that the ride has been completed.             |
| `error`          | `{ message }` | Sends an error message to the client.                           |



