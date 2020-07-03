FROM node:14.5.0

# install sudo
RUN set -ex; \
  apt-get update; \
  DEBIAN_FRONTEND=noninteractive \
  apt-get install -y --no-install-recommends \
  sudo

# copy and install app
WORKDIR /var/www
COPY app/package.json .
COPY app/package-lock.json .
RUN npm ci
COPY app .

CMD npm start

EXPOSE 3000