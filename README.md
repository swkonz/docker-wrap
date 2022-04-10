# docker-wrap
Tool for wrapping projects in docker and launching with docker-compose

# Notes on creating a project with this setup

- First need to install docker on the machine:
    - This can be easy on mac, but is a bit more involved on ubuntu. Follow the instructions on the docker website below
    - [Install docker engine](https://docs.docker.com/engine/install/ubuntu/)
    - [Install docker compose](https://docs.docker.com/compose/install/)
- Then, need to create a `docker-compose.yaml` file that contains your app's configuration. I copied this from my portfolio template project and didn't really need to change anything
- Once the compose file is defined, you need to start a shell in the container. This is somewhat annoying. The default `node:lts-stretch` image launches a node REPL by default. To avoid this, you can override the startup command in the image by defining a mundane startup command like `command: sh`. An even better way to open the terminal is to use the command `docker-compose run --rm myapp`.
- Once we're in, we can setup a project in our repository, but first we need to install the framework cli tool (Vue/cli for Vue. Create react app for react)
- Once in a shell, install vue/cli using the instructions [here](https://cli.vuejs.org/guide/installation.html)
- After all the project files are generated, the permissions on those files will match the permissions of the docker user group (usually root). This will be problematic when we actually start writing code. To fix this, we should set all the permissions on all files in the root folder to not require root access.
```
sudo chown -R sean:sean *
sudo chown -R sean:sean .*
```


## Common issues

- Docker is installed with root privileges by default. In order to be able to run docker commands without using sudo, you should setup a new user for docker. The instructions [here are helpful](https://stackoverflow.com/questions/48957195/how-to-fix-docker-got-permission-denied-issue)
