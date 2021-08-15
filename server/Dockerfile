FROM node:14.14.0-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

CMD ["npm","run","start"]
#"start" -command that has been created in "package.json" file