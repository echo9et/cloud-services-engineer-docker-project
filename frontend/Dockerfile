# 1. Используем легковесный базовый образ для сборки фронта
FROM node:20-alpine

# 2. Устанавливаем рабочую директорию внутри контейнера
WORKDIR /app

COPY package.json package.json
COPY package-lock.json package-lock.json

RUN npm ci

RUN npx browserslist@latest --update-db

COPY . .

ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm run build -- --no-clean

CMD [""]