### Parent Repository README

# Project Name

## Overview

This project consists of two submodules (front-end and back-end) and a parent repository, all orchestrated using Docker Compose. The front-end module has separate Dockerfiles for development and production environments. This README provides instructions on how to build and run the entire application using Docker Compose.

## Repository Structure

```
project-root/
├── docker-compose.yml
├── .env-template
├── back/
│   ├── Dockerfile
│   ├── docker-compose.yml
│   ├── .env-template
│   └── ...
│
├── front/
│   ├── Dockerfile.dev
│   ├── Dockerfile.prod
│   ├── docker-compose.yml
│   ├── .env-template
│   └── ...
│
└── README.md
```

## Prerequisites

- Docker Engine

## How to Build and Run

### 1. Clone the Repository

Clone the parent repository along with its submodules:

```sh
git clone --recurse-submodules <repository-url>
cd project-root
```

### 2. Create the .env File

Copy the `.env-template` file from the parent and each submodule to create the required `.env` files:

```sh
cp .env-template .env
cd back
cp .env-template .env
cd ../front
cp .env-template .env
cd ..
```

Ensure the `.env` files contain the necessary environment variables. Modify values as needed for your setup.

### Important Note

When running the front-end in Docker (or in any environment where frontend and backend apps run on different hosts), set `NEXT_PUBLIC_ACTIVE_PROFILE` and `SPRING_PROFILE_ACTIVE` to `dev` in corresponding `.env` files due to specifics of cross-origin cookie sharing requiring HTTPS communication for `SameSite=None` cookies that are used for authentication.

### 3. Run the Entire Application

To run the entire application, including both submodules, use the `docker-compose.yml` file located in the project root:

```sh
docker-compose up --build
```

## Optional: Run Submodules Individually

### 1. Build and Run Only the Back-end

Navigate to the `back` directory and build the Docker image:

```sh
cd back
docker-compose up --build
```

### 2. Build and Run Only the Front-end

#### Development Environment

Navigate to the `front` directory and build the Docker image for development:

```sh
cd front
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up --build
```

#### Production Environment

For production, use the production Dockerfile:

```sh
cd front
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up --build
```

## Stopping the Containers

To stop the running containers, use the following command from the respective directories:

```sh
docker-compose down
```

## Cleaning Up

To remove all containers, networks, and volumes created by Docker Compose, use:

```sh
docker-compose down -v
```

## Troubleshooting

If you encounter issues, please ensure:

- Docker and Docker Compose are correctly installed and running.
- You have cloned the repository with submodules.
- The `.env` files are properly configured.

For further assistance, please refer to the Docker and Docker Compose documentation.
