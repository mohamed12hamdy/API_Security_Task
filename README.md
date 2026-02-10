API SECURITY AUTOMATION ASSESSMENT
=================================

Overview
--------
This project demonstrates automated security testing for REST APIs using
Postman collections executed via Newman and integrated into a CI/CD pipeline
using GitHub Actions.

The objective is to think like an ethical hacker and attempt to identify
potential API security weaknesses such as:
- Broken authentication or authorization
- Business logic vulnerabilities
- Input validation issues
- Injection attempts
- Sensitive data exposure

AI tools (such as OpenAI) were used to help generate negative and security-
focused test cases and attack scenarios.

--------------------------------------------------

Tech Stack
----------
- API Testing: Postman
- Automation Runner: Newman
- CI/CD: GitHub Actions
- Scripting: Postman Pre-request & Test Scripts
- AI Assistance: OpenAI (for test ideas & payload generation)

--------------------------------------------------

Tested APIs
-----------

API #1: Create Pickup
---------------------
Endpoint:
POST /api/v2/pickups

Description:
This API allows businesses to create a pickup request and automatically deduct
pickup fees from the business wallet.

Security Test Scenarios:
- Invalid / expired authorization token
- Missing authorization header
- IDOR attempts by modifying businessLocationId
- Business logic abuse (negative or very large numberOfParcels)
- Invalid scheduled dates (past / far future)
- Input validation for email and phone fields

--------------------------------------------------

API #2: Update Bank Info
-----------------------
Endpoint:
POST /api/v2/businesses/add-bank-info

Description:
Used by businesses to update bank account details for cashout transfers.

Security Test Scenarios:
- OTP validation bypass
- Incorrect or reused OTP
- Unauthorized bank info update
- Token expiration handling
- Injection attempts in bankName and beneficiaryName
- Invalid IBAN and account number formats
- Sensitive data exposure in API responses

Token Generation:
If the access token is expired, the following endpoint is used:
POST /api/v2/users/generate-token-for-interview-task

--------------------------------------------------

API #3: Forget Password
----------------------
Endpoint:
POST /api/v2/users/forget-password

Description:
Sends a password reset link to the user's email.

Security Test Scenarios:
- Email enumeration
- Rate limiting absence
- Invalid email formats
- Injection attempts in email field
- Response consistency for valid vs invalid emails

--------------------------------------------------

Automation Approach
-------------------
- All APIs are tested using Postman collections
- Security and negative scenarios are implemented using:
  - Pre-request scripts
  - Postman test assertions
- Environment variables are used for:
  - Tokens
  - Base URLs
  - Dynamic data
- Newman is used to execute the collections in headless mode

--------------------------------------------------

CI/CD Integration
-----------------
CI/CD is implemented using GitHub Actions.

Pipeline Workflow:
1. Install Node.js
2. Install Newman
3. Run Postman collection using Newman
4. Fail the pipeline if any security test fails

This ensures continuous automated security testing on every push or pull request.

--------------------------------------------------

Reports
-------
- Newman console output is used in CI logs
- Exit codes are used to fail the pipeline on test failures
- Optional HTML/JSON reports can be generated if required

--------------------------------------------------

AI Usage
--------
AI was used to:
- Generate security-focused test scenarios
- Suggest potential attack vectors
- Create edge cases and malformed payloads
- Assist in identifying business logic vulnerabilities

--------------------------------------------------

Disclaimer
----------
This project is created for assessment and educational purposes only.
All testing was performed on staging environments with permission.
No real user data was harmed or accessed.

--------------------------------------------------

Author
------
Mohamed Hamdy
API Testing & Automation Engineer
