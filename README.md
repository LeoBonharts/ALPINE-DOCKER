# Mirror Leech Telegram Bot [ MLTB ] Docker

# Warning ⚠️ Docker is Not done Yet :(
---

### Operating System `Alpine linux/amd64 & linux/arm64/v8 & linux/arm/v7`
### Operating System Version `ALpine Linux EDGE Docker Image`

[![ghcr.io](https://github.com/amirulandalib/mltb-alpine-docker/actions/workflows/github-container-deploy.yml/badge.svg)](https://github.com/amirulandalib/mltb-alpine-docker/actions/workflows/github-container-deploy.yml)

## Instructions for inserting the image On anasty17/mltb 🧰

[Base dockerfile for Anasty17/MLTB](https://github.com/anasty17/mirror-leech-telegram-bot/blob/master/Dockerfile)

## Editing Instructions :

### Replace the contents Dockerfile of that like this given below 👇

---
```

FROM ghcr.io/amirulandalib/mltb-alpine-docker:latest

COPY . .

RUN pip3 install --no-cache-dir -r requirements.txt

CMD ["bash", "start.sh"]

```
---



## why using Alpine As docker image when there is Ubuntu? 🤔
 
---

 ✓ Docker image is light and could be started from scratch.

 ✓ Less ram usage ... Ideal for 512-2gb ram devices.

 ✓ All pkg repos are also available in variety like Ubuntu so no shortage of dependencies here..

---


## For support contact on issues or [here](https://t.me/kangershub)



