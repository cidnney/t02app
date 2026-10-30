# Project 2: Containerize and Run Locally

## Project Overview


Using Docker, the project demonstrates how to build and run a containerized web application. It includes a multi-stage Dockerfile, Docker Compose with Nginx and Redis services, and an AWS Lambda function that can be run locally using AWS SAM CLI.

## Prerequisites

The following tools should be installed and configured before running the project:

- Docker and Docker Compose
- AWS SAM CLI
- Ubuntu (WSL 2) terminal for Windows users

## 1. Build the Docker Image

Run the following command from the project's root directory to build the multi-stage Docker image:

`docker build -t demo:multi .`

## 2. Start the Services

Start the Nginx web server and Redis cache using Docker Compose:

`docker compose up -d`

## 3. Verify the Services

Check that both containers are running:

`docker compose ps`

The Redis cache should show a **healthy** status, while the Nginx web server should show **Up**.

Check whether Redis responds:

`docker compose exec cache redis-cli ping`

**Expected output:** `PONG`

Verify that the web server is accessible:

`curl -s -o /dev/null -w "%{http_code}\n" http://localhost:8080`

**Expected output:** `200`

## 4. Stop the Services

Stop and remove the containers and their network:

`docker compose down`

## 5. Run the AWS Lambda Function Locally

Navigate to the Lambda function directory:

`cd local-fn`

Invoke the function using AWS SAM CLI:

`sam local invoke HelloWorldFunction`

**Expected result:** The function returns `statusCode: 200` with the message `hello world`.

## 6. Test the Function with a Sample Event

Invoke the function using the provided event file:

`sam local invoke HelloWorldFunction -e events/event.json`

**Expected result:** The function returns `statusCode: 200`.

## 7. Return to the Project Directory

`cd ..`

All services and the Lambda function run locally using Docker without requiring an AWS account.
