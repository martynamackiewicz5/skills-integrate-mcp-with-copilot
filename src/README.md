# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Role-based authentication (Admin/Faculty/Student)
- Protected sign-up and unregister operations for staff users

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
| POST   | `/auth/login`                                                     | Login with username/password and receive a bearer token             |
| POST   | `/auth/logout`                                                    | Invalidate current session token                                    |
| GET    | `/auth/me`                                                        | Get current authenticated user                                      |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up a student (admin/faculty only)                              |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister a student (admin/faculty only)                           |

## Default Credentials

The application reads users from `users.json`:

- Admin: `principal` / `admin123`
- Faculty: `teacher01` / `teach123`
- Student: `student01` / `student123`

Student users can authenticate but cannot modify registrations.

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
