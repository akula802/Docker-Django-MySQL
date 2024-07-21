# Dockerfile for the Django webserver
FROM python:3

# Working dir for the code in the container
#WORKDIR /code

# Volume / mountpoint for /code, to be mounted by docker compose
VOLUME /code

# Copy the requirements.txt into the image /tmp directory
# Necessary because the code/ volume isn't mounted until docker compose builds the container
COPY ./code/requirements.txt /tmp
RUN pip install -r /tmp/requirements.txt

# Not needed as docker compose defines the RUN command
#CMD python3 /code/app/manage.py runserver
