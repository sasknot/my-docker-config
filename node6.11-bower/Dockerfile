FROM node:6.11

MAINTAINER Crane Developers

# copy all files
COPY package.json /tmp/package.json
COPY bower.json /tmp/bower.json
COPY . /app

RUN cd /tmp && npm install --quiet && npm run postinstall --quiet
RUN cp -a /tmp/node_modules /app/node_modules
RUN cp -a /tmp/bower_components /app/bower_components

WORKDIR /app/view

CMD npm start
