
# Stage 1: Build the React application using Node.js
FROM node:18-alpine AS build

# Set the working directory inside the build container
WORKDIR /app

# Copy package files first for efficient dependency caching
COPY package*.json ./

# Install frontend dependencies
RUN npm install

# Copy the frontend source files
COPY . .

# Accept the backend API URL as a build argument
ARG VITE_API_URL=http://localhost:5000

# Make the API URL available to Vite during production build
ENV VITE_API_URL=$VITE_API_URL

# Build the optimized production application
RUN npm run build


# Stage 2: Serve the production application using Nginx
FROM nginx:alpine

# Copy the production build from the Node.js stage into Nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Expose Nginx's default HTTP port
EXPOSE 80

# Keep Nginx running in the foreground
CMD ["nginx", "-g", "daemon off;"]
