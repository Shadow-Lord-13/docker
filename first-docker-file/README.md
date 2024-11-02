Project: First Dokcer file.

Steps:

- Create a app.py file with the required code for this example we are just printing "Hello!!!"

- Create a dockerfile with all the commands required to run the app.py file.

- Push your project to github.

- Create an ubuntu ec2 instance.

- ssh into the instance.

- Commands to follow after ssh into the instance:

    - Update the existing packages and install docker.

    - sudo apt update && sudo apt-get install docker.io -y

    - sudo usermod docker ubuntu
    

    - systemctl restart docker

    - docker run hello-world

    - clone the your github repo

    - Veiw your file to check if everything io correct.

    - Build docker image -> "docker build -t docker-user-name/your-image name:latest ."

    - docker images

    - docker run docker-user-name/your-image name:latest

    - docker push -u docker-user-name/your-image name:latest
