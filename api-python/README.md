## [Activity 2] Python API

1.  Make sure you have cloned the repository. If you have cloned the repository from the previous activity, just change directory to _activity-02_

    ```bash
    # change directory
    cd ../activity-02
    ```

2.  Check the _index.py_ file. This is a simple python app using flask framework.

    ```python
    import os
    from flask import Flask, jsonify

    app = Flask(__name__)

    @app.route('/health')
    def health():
        return jsonify(status="healthy")

    @app.route('/info')
    def info():
        return jsonify(
                    language="python",
                    version=os.getenv("PYTHON_VERSION"),
                    host=os.getenv("HOSTNAME")
                )

    @app.route('/')
    def hello_world():
        return f"Hello, from {(os.getenv('HOSTNAME') or 'Python')}!"

    if __name__ == '__main__':
        app.run(host="0.0.0.0", port=3001, debug=True)
    ```

    Here are the path exposed by the API.

    > a. Health Path - http://{ip}:{port}/health  
    > b. Info Path - http://{ip}:{port}/info  
    > c. Root - http://{ip}:{port}/

3.  Check the _Dockerfile_.

    ```Dockerfile
    FROM python:3.9.9-slim

    # setup app directory
    WORKDIR /app

    # copy source code
    COPY . .

    # install packages/dependencies
    RUN pip3 install -r requirements.txt

    # expose port
    EXPOSE 3001

    # run application
    CMD [ "python", "index.py"]
    ```

4.  Build the container image using the Dockerfile.

    ```bash
    # build
    docker build -t microservice-python-api:1.0 .

    # list images
    docker image ls | grep microservice-python-api
    ```

5.  Run the container image you've built in the previous step.

    ```bash
    # run
    docker run -p 8080:3001 --name python-api microservice-python-api:1.0

    # list running containers
    docker ps
    ```

6.  Access the API via command line or browser.

    ```bash
    curl http://localhost:8080/health
    # StatusCode        : 200
    # StatusDescription : OK
    # Content           : {"status":"healthy"}

    curl http://localhost:8080/info
    # StatusCode        : 200
    # StatusDescription : OK
    # Content           : {"language":"python","version":"3.9.9"}

    curl http://localhost:8080/
    # StatusCode        : 200
    # StatusDescription : OK
    ```

---

Yaay! And we're also good with the second container. Moving on to the _webtool_ and lets see how we can integrate it to the first two microservices we've created.

---

### [◀️ Prev](../activity-01#activity-1-js-api) &nbsp;&nbsp; | &nbsp;&nbsp;[Next ▶️](../activity-03#activity-3-webtool)
