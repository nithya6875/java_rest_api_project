# Task API — Spring Boot + MongoDB 

A minimal REST API to manage shell-command tasks stored in MongoDB. Locally, it runs with a normal MongoDB. 

## Features
- CRUD for `Task` documents in MongoDB
- Search by name (case-insensitive substring)
- Execute command with validation and 10s timeout
  - Local mode: runs via OS shell (dev only)
  

## Requirements
- Java 17+
- Maven 3.8+
- For local run: MongoDB on `mongodb://localhost:27017/tasksdb`

---

## 1) Run Locally (without Kubernetes)

1. Make sure MongoDB is running (Windows examples):
```powershell
# If installed as a service
Get-Service *MongoDB* | Start-Service

# Or run mongod directly (adjust version/path as installed)
"C:\Program Files\MongoDB\Server\6.0\bin\mongod.exe" --dbpath C:\data\db
```

2. Build and run the app
```bash
mvn spring-boot:run
# or build a jar
mvn -DskipTests package
java -jar target/task-api-1.0.0.jar
```

3. Test endpoints
```bash
# Create
 Invoke-RestMethod -Uri "http://localhost:8081/tasks" -Method PUT -ContentType "application/json" -Body '{ "id": "123", "name": "Print Hello", "owner": "John Smith", "command": "echo Hello World again!" }'
Note - This works only for Windows Users.
# List all
curl http://localhost:8081/tasks

# Get by id
curl "http://localhost:8081/tasks?id=123"

# Search
curl "http://localhost:8081/tasks/search?name=hello"

# Execute
curl -X PUT http://localhost:8081/tasks/123/execute

# Delete
curl -X DELETE http://localhost:8081/tasks/123
```
<img width="1671" height="570" alt="image" src="https://github.com/user-attachments/assets/3423e8b7-fd66-4b60-bced-00c6c634b942" />
<img width="1658" height="615" alt="image" src="https://github.com/user-attachments/assets/6d198c7a-8754-4efd-9bda-8fe2c6522c3b" />
<img width="1644" height="500" alt="image" src="https://github.com/user-attachments/assets/a7ee1355-3807-44f2-b74c-3e0f0db2181e" />
<img width="1590" height="631" alt="image" src="https://github.com/user-attachments/assets/5bf269cd-618a-4b42-8d45-ed6d57833131" />
<img width="1618" height="569" alt="image" src="https://github.com/user-attachments/assets/4cd3a2e2-d3d9-4464-933a-4282422465cf" />
Output is seen here
<img width="1659" height="698" alt="image" src="https://github.com/user-attachments/assets/8a09e005-c758-4839-af77-d74d76b11fd0" />




Notes
- Default server port is 8081 (see `src/main/resources/application.properties`).
- Default Mongo URI: `${MONGODB_URI:mongodb://localhost:27017/tasksdb}`.

---
