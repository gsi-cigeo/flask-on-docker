# pull official base image
FROM python:3.8.1-slim-buster

# set work directory
WORKDIR /home/developer/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Create the developer user
RUN groupadd developer && useradd -g developer developer

# install system dependencies
RUN apt-get update && apt-get install -y netcat

ENV HOME=/home/developer
ENV APP_HOME=/home/developer/app/

# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt /home/developer/app/requirements.txt
RUN pip install -r requirements.txt

# copy project
COPY . $APP_HOME

# Chown all the files to the developer user
RUN chown -R developer:developer $HOME

# Change to the developer user
USER developer

# run entrypoint.sh
ENTRYPOINT ["/home/developer/app/entrypoint.sh"]
