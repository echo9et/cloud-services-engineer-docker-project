# 1. Используем легковесный базовый образ для сборки фронта
FROM node:20-alpine AS frontend_builder

# 2. Устанавливаем рабочую директорию внутри контейнера
WORKDIR /app

COPY package.json package.json
COPY package-lock.json package-lock.json

RUN npm ci

RUN npx browserslist@latest --update-db

COPY . .

ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm run build -- --no-clean


# Nginx 
FROM nginx:1.29-alpine

COPY ./nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=frontend_builder /app/dist /usr/share/nginx/html/momo-store/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]