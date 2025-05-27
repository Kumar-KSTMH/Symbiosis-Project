# Stage 1: Build
FROM node:18-alpine AS build

WORKDIR /app
COPY nodejs-mysql-crud/package*.json ./
RUN npm install
COPY nodejs-mysql-crud/ .

# Stage 2: Runtime
FROM node:18-alpine

WORKDIR /app
COPY --from=build /app .

EXPOSE 3000
CMD ["node", "app.js"]
