FROM node:14.18.0-slim

# setup app directory
WORKDIR /usr/src/app

# copy package list
COPY package*.json ./

# install packages/dependencies
RUN npm install

# copy source code
COPY . .

# expose port
EXPOSE 3002

# run application
CMD [ "npm", "run", "start" ]
