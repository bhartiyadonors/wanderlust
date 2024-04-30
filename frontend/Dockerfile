#-------Stage 1-------#
# Base Image of NodeJS
FROM node AS Frontend

# Set Working Directory
WORKDIR /app

# Copy Source code to container
COPY . /app

#Upgrade npm version
RUN npm install -g npm@10.6.0

# Install Required Dependencies
RUN npm i

# Copy environtment file to container
COPY .env.sample .env.local

#-------Stage 2-------#
# Smaller Base Image of NodeJS
FROM node:22-slim

# Copy installed dependencies
COPY --from=Frontend /app .

# Expose port
EXPOSE 5173

# Run App
ENTRYPOINT ["npm","run"]
CMD ["dev"]
