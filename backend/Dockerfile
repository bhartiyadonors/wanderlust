FROM node:21
WORKDIR /app
COPY . .
RUN npm i
COPY .env.sample .env
EXPOSE 5000
CMD ["npm","start"]
# create here multi-stage to increase performance and reduced the file size as well
#stage1
# FROM node:21 AS backend-building
# WORKDIR /app
# COPY . .
# RUN npm i 
# #SRAGE 2
# FROM node:21-slim
# WORKDIR /app
# COPY --from=backend-building /app .
# COPY .env.sample .env 
# EXPOSE 5000
# CMD ["npm","start"]





