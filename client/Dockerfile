# Step 1: Build React app
FROM node:18-alpine AS builder

WORKDIR /app

# Copy only dependency-related files first
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the app
COPY . .

# ✅ Increase Node.js heap memory limit to avoid build crash
ENV NODE_OPTIONS=--max-old-space-size=2048

# Build React app (CRA uses /build)
RUN npm run build


# Step 2: Serve build output using Nginx
FROM nginx:alpine

# Clean existing nginx content
RUN rm -rf /usr/share/nginx/html/*

# Copy the React build output from previous stage
COPY --from=builder /app/build /usr/share/nginx/html

# Expose default Nginx port
EXPOSE 80

# Run Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
