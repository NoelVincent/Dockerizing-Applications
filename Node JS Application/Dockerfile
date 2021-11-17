FROM node:16-alpine3.12

RUN  mkdir /tmp/node-js/

WORKDIR /tmp/node-js/

COPY ./project/  .

RUN npm install

EXPOSE 8081

CMD [ "node", "server.js" ]
