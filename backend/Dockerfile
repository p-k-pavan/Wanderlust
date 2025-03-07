FROM node:18

WORKDIR /app

# Copy package.json and package-lock.json first to leverage Docker caching
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all files into the container
COPY . .

COPY .env.sample .env
# Expose the server port
EXPOSE 5000

# Set environment variables (ensure .env is correctly mounted in docker-compose)
CMD ["npm", "start"]
