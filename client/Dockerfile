# Step 1: Build Stage
FROM node:18-alpine AS builder

# Set working directory
WORKDIR /app

# Copy only the package files to install dependencies
# COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all project files
COPY . .

# Build the project (for production)
RUN npm run build

# Step 2: Serve with Nginx
FROM nginx:alpine

# Remove default nginx static content
RUN rm -rf /usr/share/nginx/html/*

# Copy the build output to Nginx's root directory
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose port 80 for the container
EXPOSE 80

# Run Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
