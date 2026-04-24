# Combined Node.js API Project (Test Cases 3, 4, & 5)

This repository combines the setup and integration from Test Cases 3, 4, and 5.

---

## Test Case 3 — Node.js Application Setup & Git Integration
Scenario: You are setting up a new Node.js REST API from scratch and publishing it to GitHub.

### Tasks
- Initialize a new Node.js project and install the required dependencies: `express` and `@types/express` (as a dev dependency).
- Create an `index.js` file that starts an Express server on port 8080 with the following endpoint:
  `GET /health` — returns HTTP status 200 with the JSON response `{ "status": "OK" }`.
- Initialize a Git repository in the project folder.
- Create an initial commit with all project files.
- Create a GitHub repository named `nodejs-api` and push your code to it.

### Expected Outcome
- Project folder contains `package.json`, `node_modules/`, and `index.js`.
- Running the server locally and calling `GET /health` returns:
  `{ "status": "OK" }`
- GitHub repository `nodejs-api` is publicly visible with at least one commit containing all project files.

---

## Test Case 4 — Docker & Containerization
Scenario: The Node.js API from Test Case 3 must be packaged into a Docker container for consistent deployment.

### Tasks
- Write a Dockerfile in the project root that:
  - Uses `node:18-alpine` as the base image.
  - Sets `/app` as the working directory.
  - Copies and installs dependencies.
  - Exposes port 8080.
  - Starts the application using `node index.js`.
- Build a Docker image named `nodejs-api`.
- Run the container and verify the `/health` endpoint responds correctly on `http://localhost:8080/health`.
- Write a `docker-compose.yml` file to run the application as a background service on the same port.

### Expected Outcome
- `docker build` completes with no errors and the image appears in `docker images`.
- The container starts successfully and `GET http://localhost:8080/health` returns:
  `{ "status": "OK" }`
- `docker compose up -d` starts the service in detached mode with no errors.

---

## Test Case 5 — CI/CD Pipeline with GitHub Actions
Scenario: Your team requires an automated pipeline that runs on every code push to the main branch, installs dependencies, builds the Docker image, and simulates a deployment.

### Tasks
- Inside your `nodejs-api` repository, create the directory `.github/workflows/`.
- Create a workflow file `deploy.yml` inside that directory with the following behaviour:
  - Trigger: On every push to the main branch.
  - Runner: Ubuntu latest.
  - Steps:
    - Check out the repository code.
    - Set up Node.js version 18.
    - Install project dependencies.
    - Build the Docker image tagged as `nodejs-api`.
    - Print the message: `Deploying application to server...`
- Commit all changes with the message: "This is the new CI/CD pipeline for CA2" and push to main.
- Navigate to the Actions tab on GitHub and confirm the pipeline ran successfully.

### Expected Outcome
- `.github/workflows/deploy.yml` is present in the repository.
- The GitHub Actions run triggered by the commit shows all 5 steps completing with a green checkmark.
- No step fails; the final step prints the deploy message in the logs.
