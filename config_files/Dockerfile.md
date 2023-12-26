```yml
# Etapa 1: Construir la aplicación
FROM node:20-alpine as builder
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Etapa 2: Configurar la imagen de producción
FROM node:20-alpine
WORKDIR /usr/src/app
COPY --from=builder /usr/src/app/dist ./dist
COPY package*.json ./
RUN npm install --only=production

EXPOSE 3000
CMD ["node", "dist/main"]
```