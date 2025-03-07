FROM node:18

WORKDIR /app

COPY package*.json ./

RUN npm i

COPY . .

COPY .env.sample .env.local

EXPOSE 5173

CMD ["npm", "run", "dev", "--", "--host"]
