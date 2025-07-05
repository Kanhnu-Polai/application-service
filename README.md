# Application Service - SkillVerify
This microservice handles job application such as 
- Job application submission
- Resume uploads
- Exam scheduling
- Status tracking (Applied → Exam → Rounds → Shortlisted)

## API Endpoints
### 1. Job Application Submission
- **Method**: `POST /apply`  
- **Description**: Allows a candidate to apply for a job.
- **Request Body**:
```json
{
  "email": "user@example.com",
  "jobId": "JOB123",
  "resumeLink": "https://example.com/resume.pdf"
}
```
- **Response**:
```json
 {
   "message": "Application submitted successfully",
   "applicationId": "APP001"
 }
 ```

### 2. Get Applications by User
- **Method**: `GET /by-user/{email}`  
- **Description**: Fetch all job applications submitted by a user.
- **Response**:
```json
 [
  {
    "applicationId": "APP001",
    "jobId": "JOB123",
    "status": "Applied",
    "appliedAt": "2025-07-06T10:30:00"
  }
]
 ```

### 3. Get Applications by Job
- **Method**: `GET /by-job/{jobId}`  
- **Description**: Fetch all applications submitted for a specific job.
- **Response**:
```json
 [
  {
    "applicationId": "APP001",
    "email": "user@example.com",
    "resumeLink": "https://example.com/resume.pdf",
    "status": "Applied"
  }
]
 ```

### 4. Get Application by ID
- **Method**: `GET /{applicationId}`  
- **Description**: Get full details of a specific application.
- **Response**:
```json
 {
  "applicationId": "APP001",
  "jobId": "JOB123",
  "email": "user@example.com",
  "resumeLink": "https://example.com/resume.pdf",
  "status": "Round-1 Qualified",
  "examDate": "2025-07-10T11:00:00"
}
 ```
### 5. Update Application Status
- **Method**: `PUT /update-status`  
- **Description**: Change the status of an existing application..
- **Request Body**:
```json
{
  "applicationId": "APP001",
  "status": "Round-1 Qualified"
}
```
- **Response**:
```json
 {
  "message": "Status updated successfully"
}
 ```

### 6. Schedule Exam (via Exam Service)
- **Method**: ` PUT /schedule-exam`  
- **Description**: Triggers an internal request to the exam-service to schedule an exam for the candidate. On success, it links the scheduled exam to the application.
  🔗 This endpoint internally communicates with the Exam Service.

- **Request Body**:
```json
{
  "applicationId": "APP001",
  "examTitle": "Java Backend Assessment",
  "examDate": "2025-07-15T10:00:00",
  "durationMinutes": 60
}
```
- **Response**:
```json
 {
  "message": "Status updated successfully"
}
 ```
