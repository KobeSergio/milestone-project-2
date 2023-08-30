## [Activity 1] JS API

1.  Clone and explore the repository.

    ```bash
    # clone
    git clone https://gitlab.stratpoint.cloud/stratpoint-cloud-native/bootcamp-resources/foundational/milestone-project

    # change directory
    cd activities/activity-01

    # list and check the files
    ls
    # .dockerignore         - used to exclude files and directories
    # Dockerfile            - containes instructions in building an image
    # index.js              - entrypoint of the code
    # package.json          - nodejs metadata, includes libraries and other info
    ```

2.  Check the _index.js_ file. This is a simple nodejs app using express application framework.

    ```js
    const express = require("express");
    const app = express();
    const port = 3000;

    const logger = (data) => {
      console.log("[INFO]: ", new Date(), data);
    };

    app.get("/health", (req, res) => {
      logger("/health : " + JSON.stringify(req.headers));
      res.json({ status: "healthy" });
    });

    app.get("/info", (req, res) => {
      logger("/info : " + JSON.stringify(req.headers));
      res.json({
        language: "js",
        version: process.env.NODE_VERSION,
        host: process.env.HOSTNAME,
      });
    });

    app.get("/", (req, res) => {
      logger("/ : " + JSON.stringify(req.headers));
      res.send(
        "Hello, from " +
          (process.env.HOSTNAME ? process.env.HOSTNAME : "NodeJS") +
          " !"
      );
    });

    app.listen(port, () => {
      console.log(`Example app listening at http://localhost:${port}`);
    });
    ```

    Here are the path exposed by the API.

    > a. Health Path - http://{ip}:{port}/health  
    > b. Info Path - http://{ip}:{port}/info  
    > c. Root - http://{ip}:{port}/

3.  Check the _Dockerfile_.

    ```Dockerfile
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
    EXPOSE 3000

    # run application
    CMD [ "npm", "run", "start" ]
    ```

4.  Build the container image using the Dockerfile.

    ```bash
    # build
    docker build -t microservice-js-api:1.0 .

    # list images
    docker image ls | grep microservice-js-api
    ```

5.  Run the container image you've built in the previous step.

    ```bash
    # run
    docker run -p 80:3000 --name js-api microservice-js-api:1.0
    # -p 80:3000              # map ports - local port:container port
    # --name js-api           # set name of container
    # microservice-js-api:1.0 # image name and tag

    # list running containers
    docker ps
    # CONTAINER ID   IMAGE                     COMMAND                  CREATED              STATUS              PORTS                  NAMES
    # bf837a267ca6   microservice-js-api:1.0   "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:80->3000/tcp   js-api

    ```

    > _Note that the container id will be different from yours._

6.  Access the API via command line or browser.

    ```bash
    curl http://localhost/health
    # StatusCode        : 200
    # StatusDescription : OK
    # Content           : {"status":"healthy"}

    curl http://localhost/info
    # StatusCode        : 200
    # StatusDescription : OK
    # Content           : {"language":"js","version":"14.18.0","host":"bf837a267ca6"}

    curl http://localhost/
    # StatusCode        : 200
    # StatusDescription : OK
    # Content           : Hello, from bf837a267ca6 !
    ```

---

Great! We're done with the first container. Let's proceed with the second one - the Python API.

---

### [◀️ Prev](../../activities#build-and-deploy-microservices-using-containers) &nbsp;&nbsp; | &nbsp;&nbsp;[Next ▶️](../activity-02#activity-2-python-api)
