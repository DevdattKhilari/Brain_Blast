# Step 1: Build React app
FROM node:18-alpine AS builder

# Set working directory
WORKDIR /app

# Copy dependency files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Build the React app (output will be in /app/build)
RUN npm run build


# Step 2: Serve using Nginx
FROM nginx:alpine

# Clean default nginx static files
RUN rm -rf /usr/share/nginx/html/*

# Copy build output from builder
COPY --from=builder /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]
