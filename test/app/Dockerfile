#FROM node:18-alpine AS builde
FROM node:19.6.0 AS build

#RUN npm --version
WORKDIR /app
COPY test/app/package*.json ./
RUN npm install
COPY test/app/ .
EXPOSE 3000
RUN npm run build --prod

# Stage 2: Setup Nginx to serve Angular application
FROM nginx:1.23.4
#COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY test/app/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist/app /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
