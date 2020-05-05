# expose-docker-container
By having Docker containers, this repository is focused on exposing the localhost port of Docker through internet, leaving a local network. Now, it doesn't matter the network.

This is very usefull for every OS, but specially for Docker installed on Windows, because the VM (VirtualBox) doesn't have a direct connection to the `localhost` interface.

# Steps
- Create network @ Docker
  - `docker network create myngroknet`
- `docker pull wernight/ngrok`
- Run a container with a mapped port
  - eg: `docker run -d -p 80 –net myngroknet –name www nginx`
- Run the `ngrok` container, with the port 4040 open, for checking the open connections
  - `docker run -d -p 4040:4040 –net myngroknet –name ngrok wernight/ngrok ngrok http www:80`
  - **Note**: The command that it is executed at the `ngrok` container is `ngrok http www:80`, where
    - `www` is the name of the container
    - `80` is the open port from www
  - Go to [localhost:4040](http://localhost:4040) for checking the open connections with `ngrok`
    - Check first if your VM has the `4040` port open. Otherwise, create the connection to it.

# Reference
[Expose Docker Container services on the Internet using the ngrok docker image](https://technology.amis.nl/2019/01/06/expose-docker-container-services-on-the-internet-using-ngrok/)