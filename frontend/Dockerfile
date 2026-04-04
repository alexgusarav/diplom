FROM node:22-slim AS build
WORKDIR /app
ARG VITE_KEY_REDUX
ENV VITE_KEY_REDUX=$VITE_KEY_REDUX
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Production stage
 FROM nginx:stable-alpine
 RUN rm /etc/nginx/conf.d/default.conf
 COPY nginx.conf /etc/nginx/conf.d/default.conf
 COPY --from=build /app/dist /usr/share/nginx/html
 EXPOSE 80
 CMD ["nginx", "-g", "daemon off;"]