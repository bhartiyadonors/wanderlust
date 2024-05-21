# Base Image of NodeJS
FROM node

# Set Working Directory
WORKDIR /app

# Copy Source code to container
COPY . /app

# Install Required Dependencies
RUN npm i

# Copy environtment file to container
COPY .env.sample .env.local

# Expose port
EXPOSE 5173

# Run App
ENTRYPOINT ["npm","run"]
CMD ["dev","--","--host"]
