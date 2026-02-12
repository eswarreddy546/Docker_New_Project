FROM node:20.19.5-alpine3.21 AS build
WORKDIR /opt/server
EXPOSE 8080
COPY  package.json .
COPY *.js .

RUN npm install 
     

FROM node:20.19.5-alpine3.21 

WORKDIR /opt/server


COPY  --from=build /opt/server /opt/server

RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

RUN chown -R roboshop:roboshop /opt/server

USER roboshop

ENV MONGO=true \
     REDIS_URL='redis://redis:6379'\
     MONGO_URL="mongodb://mongodb:27017/users"

CMD [ "node","server.js" ]