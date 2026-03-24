# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities (authenticated)
- Unregister students from activities (authenticated)
- Login endpoint with role-based permissions (`admin`, `student`)

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/auth/login`                                                     | Authenticate and receive Bearer token                              |
| GET    | `/auth/me`                                                        | Validate token and return current user                             |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity (auth required)                            |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister a student (auth required)                           |

## Demo Credentials

- Admin: `teacher` / `teacher123`
- Student: `emma` / `student123`

## Authorization Rules

- Admin users can register or unregister any student email.
- Student users can register or unregister only their own email.
- Anonymous users can view activities but cannot modify registrations.

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.
