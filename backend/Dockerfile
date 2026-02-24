# Use official Node image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy package.json files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy remaining files
COPY . .

# Expose backend port
EXPOSE 8080

# Start application
CMD ["npm", "start"]