FROM node:18 AS builder
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build -- --configuration production || npm run build

FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY --from=builder /app/dist/angular-15-crud/ /usr/share/nginx/html/
CMD ["nginx", "-g", "daemon off;"]
EXPOSE 80
