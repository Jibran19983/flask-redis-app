# Simple Flask and Redis app using Docker Compose

This is a simple Flask app that keeps track of how many times you visit the website url. 


## Dockerfile

```python

FROM python:3.4-alpine

ADD . /code

WORKDIR /code

RUN pip install -r requirements.txt

CMD ["python", "app.py"]


```

This tells Docker to:

* Build an image starting with the Python 3.4 image.

* Add the current directory `.` into the path `/code` in the image.

* Set the working directory to `/code`.

* Install the Python dependencies.

* Set the default command for the container to `python app.py.

