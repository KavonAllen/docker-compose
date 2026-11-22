
# Use Node.js 18 Alpine as the lightweight base image
FROM node:18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package files first to optimize Docker layer caching
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the remaining backend application files
COPY . .

# Create a directory for persistent SQLite database storage
RUN mkdir -p /app/data

# Set the database location inside the container
ENV DB_PATH=/app/data/recipes.db

# Expose the backend API port
EXPOSE 5000

# Start the backend application
CMD ["npm", "start"]
