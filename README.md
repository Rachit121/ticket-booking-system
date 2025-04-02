# High-Performance Ticket Booking System

A scalable, high-performance system for booking movie, concert, and train tickets with robust concurrency handling to prevent double bookings.

## Features

- **User Management**: Registration, authentication, and authorization using Spring Security with JWT
- **Event Management**: Create, update, and search for various events (movies, concerts, trains)
- **Seat Management**: Different seat categories with real-time availability
- **Booking System**: Concurrent booking with optimistic locking to prevent double bookings
- **Caching**: Redis for caching seat availability to reduce database load
- **Asynchronous Processing**: Kafka for processing reservations and sending confirmations

## Technology Stack

- **Backend**: Spring Boot, Spring Security, Spring Data JPA
- **Database**: PostgreSQL
- **Caching**: Redis
- **Message Broker**: Kafka
- **Authentication**: JWT (JSON Web Tokens)
- **Containerization**: Docker, Docker Compose

## System Architecture

- **Optimistic Locking**: Prevents double booking of seats
- **Redis Caching**: Stores seat availability to avoid frequent DB hits
- **Kafka**: Handles high-traffic booking events asynchronously

## Prerequisites

- Java 17+
- Maven
- Docker and Docker Compose

## Setup and Installation

1. Clone the repository:
```
git clone https://github.com/yourusername/ticket-booking-system.git
cd ticket-booking-system
```

2. Start the required services using Docker Compose:
```
docker-compose up -d
```

3. Build and run the application:
```
mvn clean install
java -jar target/ticket-booking-system.jar
```

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login and get JWT tokens
- `POST /api/auth/refresh` - Refresh access token

### Events
- `GET /api/events` - Get all events (paginated)
- `GET /api/events/{id}` - Get event by ID
- `GET /api/events/type/{type}` - Get events by type
- `GET /api/events/search` - Search events by criteria
- `POST /api/events` - Create a new event (admin)
- `PUT /api/events/{id}` - Update an event (admin)
- `DELETE /api/events/{id}` - Delete an event (admin)

### Seats
- `GET /api/seats/event/{eventId}` - Get available seats for an event
- `GET /api/seats/event/{eventId}/category/{category}` - Get available seats by category
- `GET /api/seats/event/{eventId}/availability` - Get seat availability by category
- `POST /api/seats/event/{eventId}` - Create a seat (admin)
- `PUT /api/seats/{id}` - Update a seat (admin)
- `DELETE /api/seats/{id}` - Delete a seat (admin)

### Bookings
- `POST /api/bookings` - Create a booking
- `GET /api/bookings` - Get current user's bookings
- `GET /api/bookings/{id}` - Get booking by ID
- `GET /api/bookings/event/{eventId}` - Get bookings by event (admin)
- `DELETE /api/bookings/{id}` - Cancel a booking

### Users
- `GET /api/users/profile` - Get current user profile
- `PUT /api/users/profile` - Update current user profile
- `GET /api/users` - Get all users (admin)
- `GET /api/users/{id}` - Get user by ID (admin)
- `PUT /api/users/{id}/roles` - Update user roles (admin)
- `DELETE /api/users/{id}` - Delete a user (admin)

## Concurrency Handling

The system uses multiple strategies to handle concurrent bookings:

1. **Optimistic Locking**: Entity version checking prevents conflicts
2. **Redis Caching**: Maintains real-time seat availability
3. **Kafka Message Queue**: Processes booking requests asynchronously

