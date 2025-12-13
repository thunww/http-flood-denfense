FROM node:20 AS build
WORKDIR /app

COPY package*.json ./

# Cài từng bước để dễ debug
RUN npm cache clean --force
RUN npm install --legacy-peer-deps --loglevel verbose

COPY . .
RUN npm run build

FROM nginx:stable-alpine
COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]