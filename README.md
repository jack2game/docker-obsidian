# docker-obsidian

A docker image for [Obsidian.md](https://obsidian.md/) using the [linuxserver.io](https://linuxserver.io/)'s KASM base image.

## Usage

Here are some example snippets to help you get started creating a container.

### docker-compose (amd64)

```yaml
WEB_PORT=12345
rm -rfv $HOME/docker/obsidian/config
mkdir -p $HOME/docker/obsidian/vaults
mkdir -p $HOME/docker/obsidian/config

IMAGE_NAME=docker-obsidian:latest
sudo docker run -d --name obsidian \
  --restart=unless-stopped \
  -e PUID=1000 \
  -e PGID=1000 \
  -p 127.0.0.1:$WEB_PORT:8080 \
  --userns=host \
  -e TZ=Asia/Hong_Kong \
  -e SUBFOLDER="/obsidian/" \
  -v $HOME/docker/obsidian/config:/config \
  --mount type=bind,src=$HOME/docker/obsidian/vaults,dst=/vaults,bind-propagation=rshared \
  --mount type=tmpfs,destination=/tmp \
  ${IMAGE_NAME}
```

### docker-compose (arm64)

```yaml
WEB_PORT=12345
rm -rfv $HOME/docker/obsidian/config
mkdir -p $HOME/docker/obsidian/vaults
mkdir -p $HOME/docker/obsidian/config

IMAGE_NAME=docker-obsidian:latest
sudo docker run -d --name obsidian \
  --restart=unless-stopped \
  -e PUID=1000 \
  -e PGID=1000 \
  -p 127.0.0.1:$WEB_PORT:8080 \
  --userns=host \
  -e TZ=Asia/Hong_Kong \
  -e SUBFOLDER="/obsidian/" \
  -v $HOME/docker/obsidian/config:/config \
  --mount type=bind,src=$HOME/docker/obsidian/vaults,dst=/vaults,bind-propagation=rshared \
  --mount type=tmpfs,destination=/tmp \
  --security-opt seccomp=unconfined \
  ${IMAGE_NAME}
```

## Development

User the test file to build the container using the following command.

```bash
# builds and starts the container
# container is accessible using http://localhost:8080
docker compose -f docker-compose-test.yml up
```

### Credits

 * [Sytone](https://github.com/sytone/obsidian-remote) for the initial implementation of this.
 * [ilkersigirci](https://github.com/ilkersigirci) and [this issue](https://github.com/sytone/obsidian-remote/issues/51) which helped form the base of the Dockerfile.
