## Microservices_Containerization_Assessment
Objective - Containerize a microservices-based application using Node.js, Docker, and Docker Compose.

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
#### 1. Go to root directory and run `docker compose build` command
<img width="1876" height="206" alt="image" src="https://github.com/user-attachments/assets/79b0487e-cd03-4dab-99b4-0365c2fe28b5" />
<img width="1202" height="262" alt="image" src="https://github.com/user-attachments/assets/1df1d1a6-2faa-4048-a03e-fc909cf81498" />

#### 2. Once the build is completed, start the containers using `docker compose up` command
<img width="1447" height="321" alt="image" src="https://github.com/user-attachments/assets/3b5b941a-fefd-4522-879f-6d6c6624cab0" />
<img width="1291" height="282" alt="image" src="https://github.com/user-attachments/assets/e8b13419-4669-4fc8-9361-483f26c583b0" />

#### 3. Once the containers are created, check running containers using `docker ps` command
<img width="1457" height="263" alt="image" src="https://github.com/user-attachments/assets/c76f9a9b-2654-403f-bb43-b7ddb8ecf308" />

#### 4. Also check the logs using `docker compose logs`, `docker compose logs -f` commands
<img width="1452" height="332" alt="image" src="https://github.com/user-attachments/assets/dfd562f4-9f22-458e-8f18-ca5dbbd5f753" />

### Task 4: Testing the outputs
#### 1. To get the required outputs we have updated the `app.js` file and added a extra line to give the result `User Service is running` when reaching the local host `http://localhost:3000/` from browser. The same has been updated for Product, Order and Gateway services accordingly. 
```
app.get('/', (req, res) => {
    res.send('User Service is running');
});
```
#### 2. Result for User service when connecting with `http://localhost:3000/` and `http://localhost:3000/users`
<img width="505" height="211" alt="image" src="https://github.com/user-attachments/assets/95c25b68-5434-49ba-bd6a-1a86d7edfae5" />
<img width="463" height="380" alt="image" src="https://github.com/user-attachments/assets/79889fdd-e284-4b37-9f3c-d9ff106febe4" />
<img width="486" height="221" alt="image" src="https://github.com/user-attachments/assets/cb450dab-e2cf-44ec-8322-021f8c29ba76" />

#### 3. Result for Product service when connecting with `http://localhost:3001/` and `http://localhost:3001/products`
<img width="332" height="255" alt="image" src="https://github.com/user-attachments/assets/d4d1f52f-d54b-46fd-9130-27aed28cdadc" />
<img width="400" height="387" alt="image" src="https://github.com/user-attachments/assets/0347f2c8-379b-40d2-9359-959f1ab4d3e7" />

#### 3. Result for Order service when connecting with `http://localhost:3002/` and `http://localhost:3002/order`
<img width="318" height="232" alt="image" src="https://github.com/user-attachments/assets/8744334f-19ab-4a2f-af64-32e96b757bdd" />
<img width="386" height="265" alt="image" src="https://github.com/user-attachments/assets/5d2f8077-f011-46e5-ba3e-f71cef15bfbd" />

#### 4. Result for Gateway service when connecting with `http://localhost:3003/` and `http://localhost:3003/health`
<img width="337" height="267" alt="image" src="https://github.com/user-attachments/assets/2f3a8513-9a4b-4ed7-b436-ba4c12a0f89e" />
<img width="400" height="291" alt="image" src="https://github.com/user-attachments/assets/adae144d-e3ce-4555-8110-e4918c4ef0d1" />
<img width="415" height="387" alt="image" src="https://github.com/user-attachments/assets/12a539d5-08bc-4fe0-b910-d2653d3203ba" />

#### 5. Now to check if the communications between the containers are working:
1. Run `docker exec -it gateway-service sh` to open a shell inside the Gateway container
2. From within the container, test connectivity to the User Service using `wget -qO- http://user-service:3000` command
3. This confirms that the services can communicate over the shared Docker network
<img width="1111" height="76" alt="image" src="https://github.com/user-attachments/assets/c58f0087-e8d9-451f-9c19-29e733f012af" />

### Finally after getting all the required outputs and once the code is working, stop and remove the running containers `docker compose down -v`
<img width="1460" height="213" alt="image" src="https://github.com/user-attachments/assets/70cc3aed-a7dd-4bdf-8dfa-3287bec7881f" />


## This completes the assignment and all the required screenshots along with the codes, docker file attached in the same repository
