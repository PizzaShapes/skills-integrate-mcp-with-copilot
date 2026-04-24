# Mergington High School Activities API

A super simple FastAPI application that allows students to view extracurricular activities while teachers manage registrations.

## Features

- View all available extracurricular activities
- Teacher login backed by a JSON credential file
- Register students for activities
- Unregister students from activities

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   uvicorn app:app --reload
   ```

3. Open your browser and go to:
   - App: http://localhost:8000/
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## Teacher Access

Teacher credentials are stored in `teachers.json`.

Sample accounts:

- `principal@mergington.edu` / `mergington-admin`
- `coach.taylor@mergington.edu` / `falcons-rule`

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| GET    | `/auth/session`                                                   | Check whether a teacher is currently signed in                      |
| POST   | `/auth/login`                                                     | Sign in as a teacher and create an authenticated session            |
| POST   | `/auth/logout`                                                    | End the current teacher session                                     |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Register a student for an activity                                  |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Remove a student from an activity                                |

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

Activity data and teacher sessions are stored in memory, which means changes are reset when the server restarts.
