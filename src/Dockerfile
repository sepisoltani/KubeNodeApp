# Use the official Node.js image
FROM node:18

# Create and change to the app directory
WORKDIR /usr/src/app

# Copy application dependency manifest files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application files
COPY . .

# Start the app
CMD [ "node", "app.js" ]

# Inform Docker that the container listens on port 3000
EXPOSE 3000
