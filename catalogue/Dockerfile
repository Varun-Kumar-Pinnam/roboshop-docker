FROM node:20.20.2-alpine3.23 AS builder
WORKDIR /app
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.20.2-alpine3.23
WORKDIR /app
EXPOSE 8080
COPY --from=builder /app /app
ENV MONGO="true"\
    MONGO_URL="mongodb://mongodb:27017/catalogue"
RUN addgroup -s roboshop && adduser -s roboshop -G roboshop
RUN chowon -R roboshop:roboshop /app
USER roboshop
CMD ["node","server.js"]



##### node:20 consumes more space 
# FROM node:20
# WORKDIR /app
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO="true"\
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node","server.js"]