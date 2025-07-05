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

