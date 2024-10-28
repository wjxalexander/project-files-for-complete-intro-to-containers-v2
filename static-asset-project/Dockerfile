FROM node:23 AS node-Builder
RUN mkdir /app
WORKDIR /app
COPY . .
RUN npm ci
RUN npm run build

FROM nginx
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./default.conf /etc/nginx/conf.d/default.conf
COPY ./certs /etc/nginx/certs
COPY --from=node-builder /app/dist /usr/share/nginx/html

# docker build --tag my-static-project:1.0 .
# docker run -it -p 8080:80 --name my-app --rm --init my-static-project:1.0