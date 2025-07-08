FROM node:18.17.0 AS build

WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx:latest
COPY --from=build /app/build /usr/share/nginx/html
