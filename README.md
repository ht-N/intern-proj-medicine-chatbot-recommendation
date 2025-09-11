
# FPT Medicine Chatbot – Docker Installation Guide

## System Requirements
- Docker installed (Docker Desktop on Windows/macOS, Docker Engine on Linux)
- Docker Compose installed (already included in Docker Desktop)
- (Optional) NVIDIA GPU if you want to enable GPU acceleration for Ollama

## 1. Download the Source Code
```bash
git clone <repo_url>
cd project
````

## 2. Install Docker
Below is the guide to install Docker for Ubuntu:

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
````

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
````

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
````



## 3. Start the entire and install the ollama model (for local embedding (this save cost))

Start the container first in order to got n8n, qdrant and ollama running:

```bash
docker-compose up -d
```

When all of it got running, install the local embedding model:

```bash
docker exec -it ollama ollama pull mxbai-embed-large
```

## 4. Access the Services

* n8n: [http://localhost:5678](http://localhost:5678)
* Qdrant REST API: [http://localhost:6333](http://localhost:6333)
* Ollama API: [http://localhost:11434](http://localhost:11434)

## Useful Commands

* View logs: `docker-compose logs -f`
* Stop services: `docker-compose down`
* Restart services: `docker-compose restart`

If you encounter issues, make sure Docker is running, ports 5678/6333/11434 are not in use, and try restarting the containers.
