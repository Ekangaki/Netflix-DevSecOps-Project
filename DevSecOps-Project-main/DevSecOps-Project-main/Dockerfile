FROM node:16.17.0-alpine as builder
WORKDIR /app
COPY ./DevSecOps-Project-main/DevSecOps-Project-main/package.json .
COPY ./DevSecOps-Project-main/DevSecOps-Project-main/yarn.lock .
RUN yarn install
COPY . .
ARG TMDB_V3_API_KEY
ENV VITE_APP_TMDB_V3_API_KEY=${TMDB_V3_API_KEY}
RUN yarn cache clean
RUN yarn set version latest
RUN yarn build


FROM nginx:stable-alpine
WORKDIR /usr/share/nginx/html
RUN rm -rf ./*
COPY --from=builder /app/dist .
EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]
