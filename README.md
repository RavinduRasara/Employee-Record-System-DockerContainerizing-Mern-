&nbsp;

**<span style="color: rgb(224, 62, 45);">1\. Clone the Project</span>**

**<span style="color: rgb(224, 62, 45);">2\. Docker File(Front End)</span>**

```
FROM node:18.9.1

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 5173

CMD ["npm", "run", "dev"]
```

**<span style="color: rgb(224, 62, 45);">3\. Create  docker image (Frontend)</span>**

```
/MERN-docker-compose/mern/frontend$ docker build -t mern-frontend .
[+] Building 2697.3s (10/10) FINISHED                                                                                                                                                docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                                                                 0.1s
 => => transferring dockerfile: 160B                                                                                                                                                                 0.0s
 => [internal] load metadata for docker.io/library/node:18.9.1                                                                                                                                       4.8s
 => [internal] load .dockerignore                                                                                                                                                                    0.1s
 => => transferring context: 2B                                                                                                                                                                      0.0s
 => [1/5] FROM docker.io/library/node:18.9.1@sha256:d6ed353d022f6313aa7c3f3df69f3a216f1c9f8c3374502eb5e6c45088ce68e8                                                                              1538.9s
 => => resolve docker.io/library/node:18.9.1@sha256:d6ed353d022f6313aa7c3f3df69f3a216f1c9f8c3374502eb5e6c45088ce68e8                                                                                 0.1s
 => => sha256:b5fe9b6d9a2e764ea75cbd9b415d04e0053fc271fe3b59910233f126d17dc6bb 455B / 455B                                                                                                           1.0s                                                                                        1.4s
 => => sha256:8ffa7aaef4041744c03222b6b241a78a3b4ab9e8a8b99fb633a1f14b42f8bc56 196.85MB / 196.85MB                                                                                                1524.3s                                                                                                 67.7s
 => => sha256:23858da423a6737f0467fab0014e5b53009ea7405d575636af0c3f100bbb2f10 55.03MB / 55.03MB                                                                                                   765.7s
 => => extracting sha256:23858da423a6737f0467fab0014e5b53009ea7405d575636af0c3f100bbb2f10                                                                                                            2.4s
 => => extracting sha256:326f452ade5c33097eba4ba88a24bd77a93a3d994d4dc39b936482655e664857                                                                                                            1.3s
 => => extracting sha256:a42821cd14fb31c4aa253203e7f8e34fc3b15d69ce370f1223fbbe4252a64202                                                                                                                                                                                                                     3.9s
 => => extracting sha256:15346274192fa7bd25310a80f1cadb97557be8f597e20046797904d118a4a79d                                                                                                            0.1s
 => => extracting sha256:b5fe9b6d9a2e764ea75cbd9b415d04e0053fc271fe3b59910233f126d17dc6bb                                                                                                            0.0s
 => [internal] load build context                                                                                                                                                                    0.2s
 => => transferring context: 285.52kB                                                                                                                                                                0.0s
 => [2/5] WORKDIR /app                                                                                                                                                                               1.6s
 => [3/5] COPY package.json .                                                                                                                                                                        0.4s
 => [4/5] RUN npm install                                                                                                                                                                         1065.5s
 => [5/5] COPY . .                                                                                                                                                                                   1.1s 
 => exporting to image                                                                                                                                                                              84.1s 
 => => exporting layers                                                                                                                                                                             62.0s 
 => => exporting manifest sha256:2493f21a612a95a681107e67792ee19ad951adc4ff7c5fbf4fe9a5a492ce4912                                                                                                    0.1s 
 => => exporting config sha256:11a9f7d5d5c47eb404025b6d0ba95fc8a56952f9e1bccb5f9dcc5d66a3b89f94                                                                                                      0.1s
 => => exporting attestation manifest sha256:5955b558128649a274dd08d4384100e15508d7febac1f7b47411b4bdc9a0043e                                                                                        0.1s
 => => exporting manifest list sha256:c1da500144e12ef4522b223cf667cff3198a31d6a9603067ef3fc34a5d2b5d22                                                                                               0.1s
 => => naming to docker.io/library/mern-frontend:latest                                                                                                                                              0.0s
 => => unpacking to docker.io/library/mern-frontend:latest                                                                                                                                          21.5s


```

**<span style="color: rgb(224, 62, 45);">4\. Check Docker Images</span>**

```
/MERN-docker-compose/mern/frontend$ docker images
                                                                                                                                                                                      i Info →   U  In Use
IMAGE                  ID             DISK USAGE   CONTENT SIZE   EXTRA
mern-frontend:latest   c1da500144e1       2.68GB          633MB     
```

**<span style="color: rgb(224, 62, 45);">5\. Create New Docker Network</span>**

```bash
/mern/frontend$ docker network create mern  
5c8ff14dad46799372c3d8d8236cd19dfdd5b6dc2a1213497553df64fa9e548a  

/mern/frontend$ docker network ls  
NETWORK ID NAME DRIVER SCOPE  
e9a082b1cb7d bridge bridge local  
8121700e1bc1 host host local  
5c8ff14dad46 mern bridge local  
f5907c37d3e2 none null local  
b0723eca6821 secure-network bridge local
```

**<span style="color: rgb(224, 62, 45);">6\. Run Docker Container With Network</span>**

```
MERN-docker-compose/mern/frontend$ docker run --name=frontend --network=mern -d -p 5173:5173 mern-frontend
2b121477e7740397a60af68ca7f424bbbb35f81e435193760e76573b0f0d22a4
```

- <span style="color: rgb(45, 194, 107);">**if we have a common network for all docker container, container communicate easily.**</span>
- <span style="color: rgb(45, 194, 107);">**Host and container  have a different network. we can connect container and host using same bridge container to run application in local host. but better if we have a common net work in between containers. so it easy to communicate front,back,data base container each other.**</span>

**<span style="color: rgb(224, 62, 45);">7\. Checking  Running Docker Containers and Logs</span>**

```bash
/mern/frontend$ docker ps
CONTAINER ID   IMAGE           COMMAND                  CREATED         STATUS         PORTS                                         NAMES
2b121477e774   mern-frontend   "docker-entrypoint.s…"   7 minutes ago   Up 7 minutes   0.0.0.0:5173->5173/tcp, [::]:5173->5173/tcp   frontend

/mern/frontend$ docker logs frontend

> client@0.1.0 dev
> vite --host 0.0.0.0

  VITE v5.4.21  ready in 381 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: http://172.19.0.2:5173/
```

8. 

```bash
mern/frontend$ docker run --network=mern --name mongodb -d -p 27017:27017 -v ~/opt/data:/data/db mongo:latest
Unable to find image 'mongo:latest' locally
latest: Pulling from library/mongo
2605962b0286: Pull complete 
817807f3c64e: Pull complete 
1e41d5f93e35: Pull complete 
01a854eada6f: Pull complete 
8d1d6859a473: Pull complete 
3a5c9bc3c6a6: Pull complete 
0c85015575ad: Pull complete 
8d1d6859a473: Downloading [===============================================>   ]  291.5MB/305.6MB
8d1d6859a473: Downloading [===============================================>   ]  291.5MB/305.6MB
51deed191cab: Download complete 
Digest: sha256:d343c378b5c6e2fe373174abcf4a877be0dfc721b5d0b9d582204dccb1c00b86
Status: Downloaded newer image for mongo:latest
b3b06f6c754001fa7b6ec44c4556ffed0100577594ce57525b01413b6cab6376
```

&nbsp;