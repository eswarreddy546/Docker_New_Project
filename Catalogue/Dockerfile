# ---------- Stage 1 : Build ----------
FROM node:20.19.5-alpine3.21 AS build

WORKDIR /opt/server

COPY package.json .
COPY *.js .

RUN npm install


# ---------- Stage 2 : Runtime ----------
FROM node:20.19.5-alpine3.21

WORKDIR /opt/server

# Create non-root user and group
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

# Copy application from build stage
COPY --from=build /opt/server /opt/server

# Change ownership to non-root user
RUN chown -R roboshop:roboshop /opt/server

# Switch to non-root user
USER roboshop

LABEL created="Eswar Reddy"\
      maintainer="eswar"

# Environment variables
ENV MONGO=true \
    MONGO_URL="mongodb://mongodb:27017/catalogue"

# Start application
CMD ["node", "server.js"]
