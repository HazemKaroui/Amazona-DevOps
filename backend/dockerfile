FROM node:18

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

ENV MONGODB_URI="mongodb://mongo:27017/nicedb"

CMD [ "npm", "start" ]
