FROM node:16-alpine AS builder

WORKDIR /app
COPY package*.json ./
RUN npm ci

COPY . .
ENV NODE_ENV=production VUE_APP_API_URL=/api
RUN npm run build


FROM nginx:1.29.1-alpine

EXPOSE 80

RUN rm -rf /usr/share/nginx/html/*

COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
