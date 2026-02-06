
https://github.com/coder/code-server

Guide：https://coder.com/docs/code-server/install#docker


~~~
mkdir -p ~/.config
docker run -it --name code-server -p 127.0.0.1:8080:8080 \
  -v "$HOME/.local:/home/coder/.local" \
  -v "$HOME/.config:/home/coder/.config" \
  -v "$PWD:/home/coder/project" \
  -u "$(id -u):$(id -g)" \
  -e "DOCKER_USER=$USER" \
  codercom/code-server:latest
~~~








Useful links

https://lindevs.com/install-visual-studio-code-server-inside-docker-container-in-linux



