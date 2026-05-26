# E-commerce API Testing & Bug Analysis Project

![Postman](https://img.shields.io/badge/Postman-API%20Testing-orange?logo=postman)
![REST API](https://img.shields.io/badge/REST-API-blue)
![Automation](https://img.shields.io/badge/API-Automation-success)
![QA](https://img.shields.io/badge/QA-Portfolio-lightgrey)
![CI](https://img.shields.io/badge/CI-GitHub%20Actions-black?logo=github)

---

## Project Overview

This project is a **REST API testing and bug analysis portfolio project** using the FakeStore API.

It demonstrates real-world QA skills such as:
- API functional testing
- Negative testing
- Bug identification and reporting
- Test automation execution
- CI pipeline integration (GitHub Actions + Newman)

---

## API Under Test

- API: https://fakestoreapi.com/
- Type: E-commerce Demo REST API
  - Base endpoints:
  - /products
  - /carts
  - /users
  - /auth

---

## Project Objectives

- Validate REST API endpoints
- Perform CRUD operations testing
- Identify inconsistencies and missing validations
- Execute negative test scenarios
- Automate API test execution
- Generate CI-based test reports

---

## Test Coverage

### Products
- GET all products
- GET single product
- POST new product
- PUT update product
- DELETE product

### Users
- GET users list
- GET single user
- POST create user
- PUT update user
- DELETE user

### Carts
- GET carts
- GET single cart
- GET carts by user
- POST new cart

### Authentication
- Login with valid credentials
- Login with invalid credentials

---

## Negative Testing Scenarios

- Invalid product ID
- Missing request body fields
- Empty payload submission
- Wrong data types in request
- Non-existing endpoints

---

## Bug Analysis Report

During API testing, the following issues and inconsistencies were identified:

### 1. Missing Input Validation
- API accepts incomplete or empty payloads
- Expected: validation error (400)
- Actual: success response or silent failure

### 2. Inconsistent Response Structure
- Different endpoints return different JSON formats
- No unified response schema

### 3. Weak Error Handling
- Invalid IDs sometimes return empty objects instead of proper errors

### 4. Data Persistence Limitations
- POST/PUT requests do not persist data permanently (mock behavior)

---

## Tools Used

- Postman (API testing)
- Newman (CLI execution)
- Git & GitHub
- GitHub Actions (CI/CD)

---

## Project Structure

```
ecommerce-api-testing/
│
├── collections/
│   └── fakestore-api-collection.json
│
├── environment/
│   └── environment.json
│
├── reports/
│   └── newman-report.html
│
├── .github/
│   └── workflows/
│       └── api-tests.yml
│
└── README.md
```

---

## How to Run Tests

### 📌 Run in Postman
1. Import the collection
2. Set environment variables
3. Execute using Collection Runner

---

### Run via Newman CLI

```bash
newman run collections/fakestore-api-collection.json -e environment/environment.json
```

---

### Generate HTML Report

```bash
newman run collections/fakestore-api-collection.json \
  -e environment/environment.json \
  -r cli,html
```

---

## CI Pipeline (GitHub Actions)

This project is fully CI-ready.

```yaml
name: API Test Automation

on:
  push:
    branches: [ main ]
  pull_request:

jobs:
  run-tests:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install Newman
        run: npm install -g newman newman-reporter-html

      - name: Run API Tests
        run: newman run collections/fakestore-api-collection.json -r cli,html

      - name: Upload Test Report
        uses: actions/upload-artifact@v4
        with:
          name: newman-report
          path: newman/
```

---

## Example Test Scenarios

- Verify GET /products returns 200 status and valid array
- Verify GET /products/1 returns correct product schema
- Verify POST /carts creates a new cart successfully
- Verify login fails with invalid credentials
- Verify DELETE /products/1 returns success response

---

## Key Skills Demonstrated

- REST API testing
- Test case design techniques
- Negative testing strategy
- Bug detection and documentation
- Automation with Postman & Newman
- CI/CD integration using GitHub Actions

---

## Testing Approach

- Equivalence Partitioning
- Boundary Value Analysis
- Negative Testing
- Exploratory API Testing
- Contract validation mindset

---

## Author

**Attila Tarnay**  
QA Engineer | API Testing Portfolio Project

---

## Notes

This project uses a public demo API (FakeStore).  
Data persistence is limited as expected from a mock service.
