FROM node:16-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
ENV NODE_ENV=production
RUN npm run build


FROM nginx:1.27-alpine
COPY --from=build /app/dist/frontend/ /usr/share/nginx/html
EXPOSE 80

HEALTHCHECK --interval=20s --timeout=3s --start-period=5s --retries=3 \
    CMD wget -qO- http://127.0.0.1/ || exit 1

CMD ["nginx", "-g", "daemon off;"]