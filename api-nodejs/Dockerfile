FROM node:16.13.2-alpine3.15

# adding labels
LABEL name="JS API" \
    description="This is used as backend API" \
    authors="cloud-native@stratpoint.com" \
    company="Stratpoint Technologies"

# setup app directory
WORKDIR /usr/src/app

# copy package list
COPY package*.json ./

# install packages/dependencies
RUN npm ci --only=production

# copy source code
COPY . .

# expose port
EXPOSE 3000

# set user
USER node

# run application
CMD [ "npm", "run", "start" ]
