# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Teacher-only signup and unregister controls
- Public activity roster visibility

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Configure the teacher credentials in the server environment. Do not commit credentials to the repository:

   ```
   export TEACHER_USERNAME="teacher"
   export TEACHER_PASSWORD="replace-with-a-strong-password"
   ```

3. Run the application from this directory:

   ```
   uvicorn app:app --reload
   ```

4. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

Students can view activities and participant lists without logging in. Teachers use the **Teacher login** button to manage signups. The API protects signup and unregister operations with HTTP Basic authentication; use HTTPS when deploying outside a trusted local environment. Without both credentials configured, those operations return a service-unavailable response.

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| GET    | `/auth/teacher`                                                    | Verify teacher credentials                                          |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up a student (teacher authentication required)                 |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister a student (teacher authentication required)             |

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
