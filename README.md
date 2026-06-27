# Microservices_Containerization_Assessment
Microservices Containerization Assessment

### Task 1: Create Dockerfile for Service
#### 1. Navigate to user-service folder and create a new docker file using Visual Studio
```
# Use Node.js base image
FROM node:20-alpine

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application files
COPY . .

# Expose application port
EXPOSE 3000

# Start application
CMD ["node", "app.js"]
```
<img width="737" height="570" alt="image" src="https://github.com/user-attachments/assets/1aedbd94-00f6-4209-a18e-7a53f9a6c080" />

#### 2. Navigate to product-service folder and create a new docker file using Visual Studio
```
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3001

CMD ["node", "app.js"]
```
<img width="710" height="395" alt="image" src="https://github.com/user-attachments/assets/e1b789b2-761a-4f98-81a0-30210c8dd149" />

#### 3. Navigate to order-service folder and create a new docker file using Visual Studio
```
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3002

CMD ["node", "app.js"]
```
<img width="745" height="382" alt="image" src="https://github.com/user-attachments/assets/13c0bc89-174a-42d8-9bff-2d752fbd06d7" />

#### 4. Navigate to gateway-service folder and create a new docker file using Visual Studio
```
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3003

CMD ["node", "app.js"]
```
<img width="710" height="386" alt="image" src="https://github.com/user-attachments/assets/0ac4d1ef-9a2c-4439-bcf1-c269489a1bab" />

### Task 2: Create a docker-compose.yml file
#### 1. Go back to the root folder and create a docker compose yml file
```
version: "3.9"

services:

  user-service:
    build: ./user-service
    container_name: user-service
    ports:
      - "3000:3000"
    networks:
      - microservice-network

  product-service:
    build: ./product-service
    container_name: product-service
    ports:
      - "3001:3001"
    networks:
      - microservice-network

  order-service:
    build: ./order-service
    container_name: order-service
    ports:
      - "3002:3002"
    networks:
      - microservice-network

  gateway-service:
    build: ./gateway-service
    container_name: gateway-service
    ports:
      - "3003:3003"
    depends_on:
      - user-service
      - product-service
      - order-service
    networks:
      - microservice-network

networks:
  microservice-network:
    driver: bridge
```
<img width="893" height="787" alt="image" src="https://github.com/user-attachments/assets/937d1e6b-4a58-46ec-8eae-f32c86887306" />

### Task 3: Building images and starting containers
#### 1. Go to root directory and run `docker compose build`
<img width="1876" height="206" alt="image" src="https://github.com/user-attachments/assets/79b0487e-cd03-4dab-99b4-0365c2fe28b5" />
<img width="1202" height="262" alt="image" src="https://github.com/user-attachments/assets/1df1d1a6-2faa-4048-a03e-fc909cf81498" />

2. Once the build is completed, start the containers using `docker compose up`
<img width="1447" height="321" alt="image" src="https://github.com/user-attachments/assets/3b5b941a-fefd-4522-879f-6d6c6624cab0" />
<img width="1291" height="282" alt="image" src="https://github.com/user-attachments/assets/e8b13419-4669-4fc8-9361-483f26c583b0" />

