# Wanderlust - Your Ultimate Travel Blog 🌍✈️

WanderLust is a simple MERN travel blog website ✈ This project is aimed to help people to contribute in open source, upskill in react and also master git.

![Preview Image](https://github.com/krishnaacharyaa/wanderlust/assets/116620586/17ba9da6-225f-481d-87c0-5d5a010a9538)

## [Figma Design File](https://www.figma.com/file/zqNcWGGKBo5Q2TwwVgR6G5/WanderLust--A-Travel-Blog-App?type=design&node-id=0%3A1&mode=design&t=c4oCG8N1Fjf7pxTt-1)

## [Discord Channel](https://discord.gg/FEKasAdCrG)

## 🎯 Goal of this project

At its core, this project embodies two important aims:

1. **Start Your Open Source Journey**: It's aimed to kickstart your open-source journey. Here, you'll learn the basics of Git and get a solid grip on the MERN stack and I strongly believe that learning and building should go hand in hand.
2. **React Mastery**: Once you've got the basics down, a whole new adventure begins of mastering React. This project covers everything, from simple form validation to advanced performance enhancements. And I've planned much more cool stuff to add in the near future if the project hits more number of contributors.

_I'd love for you to make the most of this project - it's all about learning, helping, and growing in the open-source world._

## Setting up the project locally

### Setting up the Backend

1. **Fork and Clone the Repository**

   ```bash
   git clone https://github.com/{your-username}/wanderlust.git
   ```

2. **Navigate to the Backend Directory**

   ```bash
   cd backend
   ```

3. **Install Required Dependencies**

   ```bash
   npm i
   ```

4. **Set up your MongoDB Database**

   - Open MongoDB Compass and connect MongoDB locally at `mongodb://localhost:27017`.

5. **Import sample data**

   > To populate the database with sample posts, you can copy the content from the `backend/data/sample_posts.json` file and insert it as a document in the `wanderlust/posts` collection in your local MongoDB database using either MongoDB Compass or `mongoimport`.

   ```bash
   mongoimport --db wanderlust --collection posts --file ./data/sample_posts.json --jsonArray
   ```

6. **Configure Environment Variables**

   ```bash
   cp .env.sample .env
   ```

7. **Start the Backend Server**

   ```bash
   npm start
   ```

   > You should see the following on your terminal output on successful setup.
   >
   > ```bash
   > [BACKEND] Server is running on port 5000
   > [BACKEND] Database connected: mongodb://127.0.0.1/wanderlust
   > ```

### Setting up the Frontend

1. **Open a New Terminal**

   ```bash
   cd frontend
   ```

2. **Install Dependencies**

   ```bash
   npm i
   ```

3. **Configure Environment Variables**

   ```bash
   cp .env.sample .env.local
   ```

4. **Launch the Development Server**

   ```bash
   npm run dev
   ```

# 🚀 Deploying Wanderlust with Docker (Without Docker Compose)

## 🛠 Step 1: Create a Docker Network

**1. Before deploying the containers, create a dedicated Docker network:**

```bash
docker network create wanderlust
```

## 🏗 Step 2: Build and Run the Frontend

**1. Navigate to the Frontend Directory:**

     ```bash
     cd frontend/
     ```

**2. Configure Environment Variables:**
If running on an AWS EC2 instance, update the API path in .env.sample:

     ```bash
     nano .env.sample
     ```

**3. Update the following line with your EC2 instance's public IP:**

     ```bash
     VITE_API_PATH=http://<EC2_PUBLIC_IP>:5000
     ```

**4. Build the Frontend Docker Image:**

     ```bash
     docker build -t frontend .
     ```

**5. Run the Frontend Container:**

     ```bash
     docker run -d --name frontend --network wanderlust -p 5173:5173 frontend
     ```

## 🗄 Step 3: Deploy MongoDB

**1. Run the MongoDB Container:**

     ```bash
     docker run -d --name mongodb --network wanderlust -p 27017:27017 mongo
     ```

**2. Copy Sample Data into MongoDB Container:**

     ```bash
     docker cp backend/data/sample_posts.json mongodb:/data/sample_posts.json
     ```

**3. Import Data into MongoDB:**

     ```bash
     docker exec -it mongodb bash
     mongoimport --db wanderlust --collection posts --file /data/sample_posts.json --jsonArray
     ```

## 🔧 Step 4: Build and Run the Backend

**1. Navigate to the Backend Directory:**

     ```bash
     cd backend/
     ```

**2. Configure Backend Environment Variables:**

     ```bash
     nano .env.sample
     ```

**3. Update the following lines:**

     ```bash
     MONGODB_URI=mongodb://mongodb/wanderlust
     CORS_ORIGIN=http://<EC2_PUBLIC_IP>:5173
     ```

**4. Build the Backend Docker Image:**

     ```bash
     docker build -t backend .
     ```

**5. Run the Backend Container:**

     ```bash
     docker run -d --name backend --network wanderlust -p 5000:5000 backend
     ```

# 🌍 Accessing the Application

**Once all containers are running, you can access the application in your browser:**

    ```bash
    http://<EC2_PUBLIC_IP>:5173
    ```

## 🏁 Summary of Running Containers

**Check running containers with:**

    ```bash
    docker ps
    ```

## If any container fails, check logs

    ```bash
    docker logs <container_name>
    ```

## Your Wanderlust travel blog is now successfully deployed using Docker! 🎉

## 📌 Setting Up Wanderlust with Docker Compose

**1 Run the Application**
    ```bash
    docker-compose up -d --build
    ```

**2. Verify Running Containers**
     ```bash
     docker ps
     ```

# 🌍 Accessing the Application

**Once all containers are running, you can access the application in your browser:**

    ```bash
    http://<EC2_PUBLIC_IP>:5173
    ```

## 🛑 Stopping & Removing Containers

**Stop all running containers**
     ```bash
     docker-compose down
     ```

**Stop and remove standalone containers**

     ```bash
     docker stop frontend backend mongodb
     docker rm frontend backend mongodb
     docker network rm wanderlust
     ```

## 🌟 Ready to Contribute?

Kindly go through [CONTRIBUTING.md](https://github.com/krishnaacharyaa/wanderlust/blob/main/.github/CONTRIBUTING.md) to understand everything from setup to contributing guidelines.
