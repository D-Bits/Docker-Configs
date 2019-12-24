FROM python:3.8-alpine

ENV PYTHONUNBUFFERED=1

# Copy the requirements file to the container, and install dependencies
COPY ./requirements.txt /requirements.txt
RUN apk add --update --no-cache postgresql-client
RUN apk add --update --no-cache --virtual .tmp-build-deps \
      gcc libc-dev linux-headers postgresql-dev
RUN pip install -r requirements.txt
RUN apk del .tmp-build-deps

# Create directory in the image for housing source code
RUN mkdir /app
WORKDIR /app
COPY ./app /app

# Create a user for running applications only
RUN adduser -D user
USER user