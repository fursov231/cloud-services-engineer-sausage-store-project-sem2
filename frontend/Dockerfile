FROM node:16-alpine AS builder

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci

COPY . .

RUN npm run build

FROM nginx:stable-alpine3.21

COPY --from=builder /app/dist/frontend /usr/share/nginx/html

RUN chown -R nginx:nginx /var/cache/nginx

CMD ["nginx", "-g", "daemon off;"]