FROM node:20.19.5-alpine3.21 AS build
WORKDIR /opt/server
COPY  package.json .
COPY *.js .

RUN npm install 



# multistage buld this is
FROM node:20.19.5-alpine3.21
WORKDIR /opt/server

COPY --from=build /opt/server /opt/server

ENV MONGO=true \
     MONGO_URL="mongodb://mongodb:27017/catalogue"

CMD [ "node","server.js" ]


