FROM node:22-alpine AS build

ARG VITE_API_URL=/api
ARG VITE_ENABLE_EVENT_MANAGEMENT=false

ENV VITE_API_URL=$VITE_API_URL \
    VITE_ENABLE_EVENT_MANAGEMENT=$VITE_ENABLE_EVENT_MANAGEMENT

WORKDIR /app

COPY frontend/package.json frontend/package-lock.json ./
RUN npm ci

COPY frontend ./
RUN npm run lint && npm run build

FROM nginx:1.29-alpine

COPY deploy/nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80
