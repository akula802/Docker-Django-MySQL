## DOCKER - DJANGO - MYSQL

### OVERVIEW

This repo enables one to bring up two containers with docker compose: a web server running Django, and a database server running MySQL. The configuration is basic, intended to get a simple development environment stood up quickly. This is not intended to deploy into a production environment.


### PREREQUISITES

You must have _Docker_ and _docker-compose_ installed in order for this to work.


### IINITIAL SETUP INSTRUCTIONS

+ Create an empty directory on your local computer, cd into it, and clone this repo.
+ Create a _.env_ file at the root where the docker-compose.yml file is.
+ Create another _.env_ file at ./web/code/app/app where the settings.py file is.
+ Populate both .env files with your secrets and other parameters. See the _sample.env_ at each location for reference.

_Note: The .env files are untracked via the .gitignore file._

Make sure you're still in the project root directory. Build the images and run the containers with:

> docker compose up -d --build

Make sure the containers are running with:

> docker ps

There should be two containers, one called 'app-web' and the other called 'app-db.' The web server waits 10 seconds before starting the Django webserver, so as to let the MySQL database(s) initialize.

At this point, you should be able to browse the new website at http://localhost:8000 

Note that a new directory will be created:

+ ./db/mysql

This directory is mounted to the 'app-db' container as a volume (at /var/lib/mysql), and stores the MySQL database files. It is untracked via the .gitignore file.


### NEXT STEPS - DJANGO

Get a shell in the webserver container and create the django superuser:

> docker exec -it app-web bash  
> python /code/app/manage.py createsuperuser

You should now be able to log in to Django's admin portal at http://localhost:8000/admin

The website code is in the ./web/code directory, which gets mounted to the 'app-web' container at /code. Work with your templates, views, urls, etc. within the local ./web/code directory.

Lastly, just tweak the .env files and settings.py as you see fit, and get to building your website.

