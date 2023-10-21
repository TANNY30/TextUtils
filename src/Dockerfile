# Use an official Node.js runtime as a parent image
FROM node:18 AS build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install project dependencies
RUN npm install

# Copy the entire project to the container
COPY . .

# Build the React app
RUN npm run build

# Use a lightweight HTTP server to serve the production build
FROM nginx:alpine

# Copy the production build from the previous stage to the webserver directory
COPY --from=build /build /usr/share/nginx/html

# Expose port 80 for the web server
EXPOSE 80

# Start the web server when the container starts
CMD ["nginx", "-g", "daemon off;"]
