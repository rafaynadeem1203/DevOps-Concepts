# MERN App with Docker

This project demonstrates how to set up and run a MERN (MongoDB, Express, React, Node.js) stack application using Docker containers.

---

## Getting Started

Follow the steps below to set up and run the application locally using Docker.

---

### 1. Clone the Repository

Clone the repository to your local machine:
```bash
git clone git@github.com:rafaynadeem1203/DevOps-Concepts.git
cd DevOps-Concepts
```

---

### 2. Pull the MongoDB Image

Pull the official MongoDB image from Docker Hub:
```bash
docker pull mongo
```

---

### 3. Run MongoDB as a Container

Run the MongoDB container with the specified username and password:
```bash
docker run --name database \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=verysecretpassword \
  -d mongo
```

---

### 4. Build and Run the Backend

1. Navigate to the `backend` folder:
   ```bash
   cd backend
   ```

2. Build the Docker image for the backend:
   ```bash
   docker build -t mern-app-backend .
   ```

3. Run the backend container:
   ```bash
   docker run --name backend \
     --network host \
     -e MONGODB_URI=mongodb://admin:verysecretpassword@localhost:27017/admin \
     -e JWT_SECRET=somethingsecret \
     -p 4000:4000 \
     -d mern-app-backend
   ```

4. Seed the database:
   Open your browser and go to:
   ```
   http://localhost:4000/api/seed
   ```
   This will populate the database with initial data.

---

### 5. Verify the Database

1. Open a terminal session inside the `database` container:
   ```bash
   docker exec -it database bash
   ```

2. Launch `mongosh` to interact with the MongoDB instance:
   ```bash
   mongosh -u admin -p verysecretpassword
   ```

3. Switch to the database and verify the data:
   ```javascript
   use admin
   db.products.find().pretty()
   db.users.find().pretty()
   ```
   Check if the seeded data is present.

---

### 6. Build and Run the Frontend

1. Navigate to the `frontend` folder:
   ```bash
   cd ../frontend
   ```

2. Build the Docker image for the frontend:
   ```bash
   docker build -t mern-app-frontend .
   ```

3. Run the frontend container:
   ```bash
   docker run --name frontend \
     --network host \
     -p 3000:3000 \
     -d mern-app-frontend
   ```

---

### 7. Access the Application

1. Open your browser and visit the React app:
   ```
   http://localhost:3000
   ```

2. The app should now display data from the backend and MongoDB.

---

## Notes

- Ensure that Docker is installed and running on your system.
- All containers must be on the same Docker network for proper communication.

---

Happy coding! 🎉

