This project includes all the docker related learnings with examples.

Commands:

- Update the existing packages and install docker.

- sudo apt update && sudo apt-get install docker.io -y

- Create django project : python -m django startproject devops

- python manage.py startapp demo (need to run this command in the same folder as manage.py file)

- docker build .

- docker images

- docker run -p 8000:8000 -it <image id>