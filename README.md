# API Testing with Postman and Jenkins

## About The Project:
This project is focused on automating API testing using Postman 👩‍🚀 and running the tests through Jenkins. The project includes a self-made API server that is used for testing API endpoints. There are 52 API tests, structured in a special way to ensure easy testing and organization.

### Tests Structure:
The Postman tests are organized into a specific structure:

```
├── Setup
│   ├── Create Admin Auth Token
│   ├── Create Not Admin Auth Token
├── /auth
│   ├── GET /auth
│   │   ├── Should return 401 when Invalid Token - GET /auth
│   │   │   ├── Before Test
│   │   │   ├── Test
│   │   │   └── After Test
│   │   │── ...   
│   │   │
│   ├── POST /auth
│   │   ├── Should return 401 when Invalid Credentials - POST /auth
│   │   │   ├── Before Test
│   │   │   ├── Test
│   │   │   └── After Test
│   │   │── ...   
│   │   │
├── /users
│   ├── Setup
│   │   ├── Generate Random User Data
│   ├── GET /users
│   │   ├── Should return 200 and Contain User IDs as Admin User - GET /users
│   │   │   ├── Before Test
│   │   │   ├── Test
│   │   │   └── After Test
│   │   │── ...   
│   │   │
│   ├── POST /users
│   │   ├── Should return 200 and Create new User as Admin User - POST /users
│   │   │   ├── Before Test
│   │   │   ├── Test
│   │   │   └── After Test
│   │   │── ...   
│   │   │
└── ...

```

1. Each folder represents an endpoint (e.g., /auth, /users).
2. Under each endpoint folder, there are subfolders for each HTTP method (e.g., GET, POST).
3. Under each HTTP method folder, there are subfolders for tests that check different scenarios related to that endpoint and method.
4. Each test folder includes three phases:
    - ✅ Before Test – setup phase
    - 🧪 Test – actual request and response verification.
    - 🧹 After Test – cleanup

### Dynamic Tests Data:
1. Every time the tests are executed, data is generated randomly to simulate a variety of scenarios.
2. The generated data is stored in collection variables, making it accessible for subsequent requests.

### About Jenkins in project:
1. Jenkins manages the entire process in a single pipeline:
    - The API server is automatically started before the tests.
    - The Postman tests are executed via Newman once the server is running.
    - All logs are captured and available in Jenkins

This approach ensures that both the API server and the Postman tests are handled automatically within the same pipeline run avoiding manual intervention.

---

## How to Run:
### Locally:
1. Install dependencies for the API server using `cd api-server && npm install`.
2. Start the server with `node server.js`.
3. Run Postman tests manually or using Newman `cd postman-api-tests && npx newman run api-tests.json`.

### In Jenkins:
1. Create pipeline script from SCM and pass correct data to the repository.
2. Build Now.

![Jenkins results](images/jenkins-results.png)
