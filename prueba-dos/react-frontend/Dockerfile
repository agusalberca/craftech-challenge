# Use an official Node.js runtime as the base image for the build process
FROM node:14 as builder

# Set the working directory inside the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package.json package-lock.json ./

# Install dependencies
RUN npm ci --production=false

# Copy the entire project to the container
COPY . .

# Build the React app
RUN npm run build

# Use an official Nginx runtime as the base image for the final image
FROM nginx:latest

# Remove default Nginx configuration
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx/nginx.conf /etc/nginx/nginx.conf

# Copy the built static files from the builder stage to the Nginx document root
COPY --from=builder /app/build /usr/share/nginx/html

# Expose port 80 to allow incoming HTTP traffic
EXPOSE 80

# Start Nginx when the Docker container launches
CMD ["nginx", "-g", "daemon off;"]