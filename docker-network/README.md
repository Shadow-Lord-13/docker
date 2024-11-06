This project only has readme file conatining all the command to under stand how Docker Netwrok work to Isolate 1 container from another.

Flow:

- Update existing poackegs and Install docker:
    - sudo apt update && sudp apt-get install docker.io -y

- Add ubuntu user to docekr group:
    - sudo usermod -aG docker ubuntu

- Relogin to the instance

- Create 2 containers named login and logout with any base image in this case we are using nginx:
    - docker run -d --name login nginx:latest
    - docker run -d --name logout nginx:latest

- Create bridge network for a continer:
    - docker network create secure-bridge

- Create container named finance with seperate bridge network named secure-network:
    - docker run --network secure-bridge --name finance -d nginx:latest

- Get IP address for each containers using inspect:
    - docker inspect login -> "IPAddress": "00.17.0.2",
    - docker inspect logout -> "IPAddress": "00.17.0.3",
    - docker inspect finance -> "IPAddress": "00.18.0.2"

- Opens an interactive Bash shell session inside the running login container
    - docker exec -it login /bin/bash

- Once in the interactive Bash shell session run the below commands to install ping:
    - apt-get update
    - apt-get install iputils-ping -y
    - ping -V -> to check if ping is installed.
    - ping <logout ip> -> Able to ping since both are in same bridge network.
    - ping <finance ip> -> Unable to ping since both are in different bridge network.


Outcome: Both container login and logout are in same default bridge network and are able to access both container, but finacne container is on different network i.e, secure-network due to this login and logput are nopt able to access finance container and vice-versa.
