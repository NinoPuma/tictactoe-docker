FROM node:20-alpine as build

WORKDIR /app
COPY . .
RUN npm install -g pnpm && pnpm install
RUN pnpm run build

FROM nginx:stable-alpine as prod
COPY nginx.conf /etc/nginx/nginx.conf

COPY --from=build /app/dist/ /usr/share/nginx/html/

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
