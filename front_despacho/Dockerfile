FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm ci
COPY . .

RUN npm run build

FROM nginx:1.25-alpine

COPY --from=build /app/nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=build /app/dist /usr/share/nginx/html

RUN touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid /var/cache/nginx /var/log/nginx /usr/share/nginx/html


USER root

EXPOSE 8080


CMD ["nginx", "-g", "daemon off;"]