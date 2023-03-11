FROM node:19-alpine AS builder
WORKDIR /app
COPY .babelrc ./
COPY package.json ./
COPY webpack*.js ./
COPY ./static/ ./static
RUN npm install
RUN npm run build

FROM nginx:1.23-alpine
COPY --from=builder /app/static/ /var/www/foodtrucks/static
COPY ./templates/ /var/www/foodtrucks/
COPY default.conf /etc/nginx/conf.d/