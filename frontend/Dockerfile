FROM node:18.17.0

WORKDIR /app

COPY . .

RUN corepack enable
RUN npm install

ENV REACT_APP_BACKEND_URL=http://backend:5000
EXPOSE 3000

CMD ["npm", "start"]

