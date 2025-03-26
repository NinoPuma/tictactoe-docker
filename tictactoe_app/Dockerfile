# Etapa de construcción
FROM node:20-alpine as build

# Establecer el directorio de trabajo
WORKDIR /app

# Copiar los archivos del proyecto
COPY . .

# Instalar pnpm y las dependencias
RUN npm install -g pnpm && pnpm install

# Construir la aplicación para producción
RUN pnpm run build

# Etapa de producción
FROM nginx:stable-alpine as prod

# Copiar configuración personalizada de Nginx
COPY nginx.conf /etc/nginx/nginx.conf

# Copiar los archivos estáticos generados al directorio de Nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Exponer el puerto 80
EXPOSE 80

# Comando para iniciar Nginx
CMD ["nginx", "-g", "daemon off;"]
