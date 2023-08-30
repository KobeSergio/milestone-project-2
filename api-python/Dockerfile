FROM python:slim

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
