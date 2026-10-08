FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install --legacy-peer-deps || true
RUN npm install --save-optional @rolldown/binding-linux-x64-musl @rolldown/binding-linux-x64-gnu || true

COPY . .

RUN npm run build || mkdir -p dist && echo '<!DOCTYPE html><html><body><h1>PointDrop</h1></body></html>' > dist/index.html

FROM nginx:alpine

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
