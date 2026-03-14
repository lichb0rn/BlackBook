---
up:
related: "[[GitHub Actions]]"
created: 2025-07-06
---
# 1. Установка GitHub Actions Runner
```sh
mkdir ~/actions-runner && cd ~/actions-runner

# Download the latest runner
curl -O -L https://github.com/actions/runner/releases/download/v2.325.0/actions-runner-linux-x64-2.325.0.tar.gz
tar xzf ./actions-runner-linux-x64-2.325.0.tar.gz

# Configure the runner (token & repo from GitHub setup)
./config.sh --url https://github.com/lichb0rn/JetSpares --token <runner-token>
```
- Токен дают в Settings -> Actions -> Runners

## Запуск в качестве демона
```sh
sudo ./svc.sh install
sudo ./svc.sh start
```

# 2. Настраиваем [[Docker]]
```sh
sudo apt install -y docker.io docker-compose
sudo usermod -aG docker $USER
newgrp docker

docker --version
docker compose version
```
