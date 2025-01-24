FROM node:18-alpine

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

ENV MONGODB_URI=mongodb://admin:verysecretpassword@database:27017/admin
ENV JWT_SECRET=somethingsecret
EXPOSE 4000

CMD ["npm", "start"]
