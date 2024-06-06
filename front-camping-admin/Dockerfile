# Stage 1: Build the Angular app
FROM node:16.10 AS build

WORKDIR /app

COPY package.json ./

RUN npm install --force

COPY . .

RUN npm run build --prod

# Stage 2: Serve the app with Nginx
FROM nginx:alpine

COPY --from=build /app/dist/ubold-angular /usr/share/nginx/html

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
