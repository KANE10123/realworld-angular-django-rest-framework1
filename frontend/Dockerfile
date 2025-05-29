# Build phase
FROM node:18 as build

WORKDIR /app

# Copy package files first for better layer caching
COPY package*.json ./
RUN npm install

# Copy rest of the application
COPY . .

# Build the app (ensure this matches your actual build setup)
RUN npm run build --configuration production

# Optional: List contents to debug
RUN ls -la /app/dist

# Serve phase
FROM nginx:alpine

# Replace default nginx config if needed (optional)
# COPY nginx.conf /etc/nginx/nginx.conf

# Copy built files from previous stage
COPY --from=build /app/dist/frontend /usr/share/nginx/html

# Expose port 80 (standard HTTP)
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
