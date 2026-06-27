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
<img width="832" height="596" alt="image" src="https://github.com/user-attachments/assets/361fa839-89ca-4841-ae40-078a07b1fb23" />

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
<img width="728" height="393" alt="image" src="https://github.com/user-attachments/assets/0fc10442-059b-4ac4-b75a-b1bc2979cc9a" />

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
<img width="693" height="412" alt="image" src="https://github.com/user-attachments/assets/c2f13759-163b-43e5-999c-90c5143737f0" />

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
<img width="746" height="372" alt="image" src="https://github.com/user-attachments/assets/5a547b5f-08a8-426b-937d-f62648f4526d" />

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
<img width="1903" height="232" alt="image" src="https://github.com/user-attachments/assets/d4992cdd-2545-4fb3-84ae-2892406ab062" />
<img width="1447" height="321" alt="image" src="https://github.com/user-attachments/assets/3b5b941a-fefd-4522-879f-6d6c6624cab0" />

