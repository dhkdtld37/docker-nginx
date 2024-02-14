# Study Docker

https://github.com/beyond-sw-camp/be01-101/issues/27

![image](https://github.com/dhkdtld37/docker-nginx/assets/149128094/083781d0-8b28-43a8-8a5b-ea882f5b3531)


## v0.2.0
- [x] push my index.html to docker hub
- https://hub.docker.com/r/dhkdtld37/nginx-my-html


## v0.3.0
- [x] deploy fly.io


## v0.4.0
- [x] push-docker-hub

## v0.4.1
- [ ] deploy-fly.io

-- -- --

### Blog to docker HUB

#### 브랜치 분리

```bash
$ git branch 0.4.0/push-docker-hub

$ git checkout 0.4.0/push-docker-hub
```

#### 도커 확인

```bash
$ sudo docker ps
$ sudo docker imgaes
```

#### 도커 허브 연동

```bash
$ sudo docker run --name BlogDockerHub -p 9055:80 -v /home/dhkdtld37/code/dhkdtld37.github.io:/usr/share/nginx/html -d nginx

$ sudo docker commit BlogDockerHub blogdh

$ sudo docker tag blogdh dhkdtld37/push-docker-hub:0.4.0

$ sudo docker push dhkdtld37/push-docker-hub:0.4.0

$ sudo docker pull dhkdtld37/push-docker-hub:0.4.0
```

#### 깃허브 PR 이후 Merge

### Deploy docker hub image to fly.io

#### 브랜치 분리

```bash
$ git branch 0.4.1/deploy-fly.io

$ git checkout 0.4.1/deploy-fly.io
```

#### Fly.io 실행

```bash
$ flyctl launch

An existing fly.toml file was found for app flydeploydhkdtld37
? Would you like to copy its configuration to the new app? No
Scanning source code
Could not find a Dockerfile, nor detect a runtime or framework from source code. Continuing with a blank app.
Creating app in /home/dhkdtld37/code/docker-nginx
We're about to launch your app on Fly.io. Here's what you're getting:

Organization: hyeonls96@naver.com    (fly launch defaults to the personal org)
Name:         docker-nginx           (derived from your directory name)
Region:       Tokyo, Japan           (this is the fastest region for you)
App Machines: shared-cpu-1x, 1GB RAM (most apps need about 1GB of RAM)
Postgres:     <none>                 (not requested)
Redis:        <none>                 (not requested)

? Do you want to tweak these settings before proceeding? Yes
failed opening browser. Copy the url (https://fly.io/cli/launch/35e443faa67acae28460fc3daf8b0516) into a browser and continue
Waiting for launch data... Done
Created app 'blogdeploydhkddltd37' in organization 'personal'
Admin URL: https://fly.io/apps/blogdeploydhkddltd37
Hostname: blogdeploydhkddltd37.fly.dev
Wrote config file fly.toml
```


#### 경로 수정

```bash
$ vi fly.toml
```

```toml
[build]
  image = "dhkdtld37/push-docker-hub:0.4.0"
```


#### 배포

```bash
$ flyctl deploy
```

#### 깃허브 PR 이후 Merge
