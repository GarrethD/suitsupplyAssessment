# suitsupplyAssessment
Postman automation assessement 


# Reqres API Postman Tests

## Introduction

This repository contains automated tests for the Reqres API using Postman and Newman. The tests cover various API endpoints to ensure they function as expected. The Postman collection includes GET, POST, and PUT requests, with data-driven tests and schema validation.

## API Overview

The Reqres API is a simple, hosted REST API for testing and prototyping. It provides endpoints for user data, including listing users, retrieving a single user, creating a user, updating a user, and more.

## API Endpoints and Test Breakdown

### 1. GET Single User Schema Validation

**Endpoint:** `GET /users/2`

**Description:** Retrieves a single user by ID and validates the response schema to ensure it matches the expected structure.

### 2. POST Create User From External Data Source

**Endpoint:** `POST /users`

**Description:** Creates a new user using data from an external CSV file. The test validates that the user is created successfully and that the response contains the expected properties, such as `id` and `createdAt`.

### 3. PUT Update User

**Endpoint:** `PUT /users/2`

**Description:** Updates an existing user with new information. The test verifies that the user information is updated correctly and that the response contains the `updatedAt` property.

## Running the Tests Locally

### Prerequisites

- Node.js and npm installed on your machine.
- Newman installed globally:
  ```sh
  npm install -g newman
  ```
  ### Clone the repository:
```sh
git clone https://github.com/yourusername/reqres-api-tests.git
cd reqres-api-tests
  ```
  ### Export your Postman collection and environment:
 Place ReqresAPITests.postman_collection.json and ReqresEnvironment.postman_environment.json in the root of the repository.
 
 ### Run the tests using Newman:
 ```sh
newman run ReqresAPITests.postman_collection.json -e ReqresEnvironment.postman_environment.json -d userdata.csv --reporters cli
  ```
  
 ## Running the Tests in GitHub Actions
 
### Steps
1. Ensure the repository contains the necessary files:

* ReqresAPITests.postman_collection.json
* ReqresEnvironment.postman_environment.json
* testData.csv
2. Create a GitHub Actions workflow:

* Create a .github/workflows directory in your repository.
* Add a YAML file named postman-tests.yml with the followi

```YAML
name: Run Postman Tests

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '16'

      - name: Install Newman
        run: npm install -g newman

      - name: Run Postman Tests
        run: |
          newman run ReqresAPITests.postman_collection.json -e ReqresEnvironment.postman_environment.json -d testData.csv --reporters cli,junit --reporter-junit-export results.xml

```
3. Push your changes to GitHub:
```sh
git add .
git commit -m "Add Postman tests and GitHub Actions workflow"
git push origin main
```
Once you push the changes, GitHub Actions will automatically trigger the workflow to run your Postman tests. You can check the status of the workflow in the "Actions" tab of your GitHub repository.

### Alternatively
You can click on and open the actions tab in this repository
Click on 'Run Postman Tests'
Run workflow.


## Conclusion
This setup ensures that your Postman tests are automatically run and validated in a CI pipeline using GitHub Actions, providing continuous integration and delivery for your API tests.
