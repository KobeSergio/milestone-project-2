## [Activity 3] Webtool

1.  Make sure you have cloned the repository. If you have cloned the repository from the previous activity, just change directory to _activity-03_

    ```bash
    # change directory
    cd ../activity-03
    ```

2.  Check the _Dockerfile_.

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
    EXPOSE 3002

    # run application
    CMD [ "npm", "run", "start" ]
    ```

3.  Build the container image using the Dockerfile.

    ```bash
    # build
    docker build -t microservice-js-web:1.0 .

    # list images
    docker image ls | grep microservice-js-web
    ```

4.  Run the container image you've built in the previous step.

    ```bash
    # run
    docker run -p 3002:3002 --name js-web microservice-js-web:1.0

    # list running containers
    docker ps
    ```

5.  Access the API via command line or browser.

    ```bash
    curl http://localhost:3002/
    # StatusCode        : 200
    # StatusDescription : OK
    # Content           : <!DOCTYPE html>
    ```

---

At this part, you should be able to curl the webtool and get _200_ response. This can also be viewed via browser.

![Webtool](../images/activity-03-webtool.png)

However, we still can''t connect to the backend APIs. You can see that **Host**, **Laguage**, and **Version** is not yet populated. In the next activity, we will integrate the webtool to the two previous APIs we've built.

---

### [◀️ Prev](../activity-02#activity-2-python-api) &nbsp;&nbsp; | &nbsp;&nbsp;[Next ▶️](../activity-04#activity-4-integration)
