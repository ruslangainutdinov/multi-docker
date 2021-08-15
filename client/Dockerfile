FROM node:alpine

WORKDIR /app

COPY ./package.json ./

RUN npm install

COPY . .

RUN npm run build


FROM nginx
# needed for AWS, cause by default for localhost it is doing nothing
EXPOSE 3000

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

COPY --from=0 /app/build /usr/share/nginx/html