
&nbsp;

**<span style="color: rgb(224, 62, 45);">1\. Clone the Project</span>**

**<span style="color: rgb(224, 62, 45);"><span style="color: rgb(255, 255, 255);">https://github.com/RavinduRasara/Employee-Record-System-DockerContainerizing-Mern-.git</span></span>**

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

&nbsp;

**<span style="color: rgb(224, 62, 45);">4\. Check Docker Images</span>**

```
/mern/frontend$ docker images
                                                                                                                                                                                      i Info →   U  In Use
IMAGE                  ID             DISK USAGE   CONTENT SIZE   EXTRA
mern-frontend:latest   c1da500144e1       2.68GB          633MB     
```

&nbsp;

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

&nbsp;

**<span style="color: rgb(224, 62, 45);">6\. Run Docker Container With Network (Front end container)</span>**

```
/mern/frontend$ docker run --name=frontend --network=mern -d -p 5173:5173 mern-frontend
2b121477e7740397a60af68ca7f424bbbb35f81e435193760e76573b0f0d22a4
```

- <span style="color: rgb(45, 194, 107);">**if we have a common network for all docker container, container communicate easily.**</span>
- <span style="color: rgb(45, 194, 107);">**Host and container  have a different network. we can connect container and host using same bridge container to run application in local host. but better if we have a common net work in between containers. so it easy to communicate front,back,data base container each other.**</span>

&nbsp;

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

&nbsp;

**<span style="color: rgb(224, 62, 45);">8\. Run Docker Container With Network (Mongo db Container)</span>**

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

**<span style="color: rgb(224, 62, 45);">9\. Checking Running Containers (Front-end and Mongodb)</span>**

```bash
/Desktop/Employee-Record-System$ docker ps
CONTAINER ID   IMAGE           COMMAND                  CREATED        STATUS          PORTS                                             NAMES
b3b06f6c7540   mongo:latest    "docker-entrypoint.s…"   43 hours ago   Up 10 seconds   0.0.0.0:27017->27017/tcp, [::]:27017->27017/tcp   mongodb
2b121477e774   mern-frontend   "docker-entrypoint.s…"   44 hours ago   Up 11 seconds   0.0.0.0:5173->5173/tcp, [::]:5173->5173/tcp       frontend
```

&nbsp;

**<span style="color: rgb(224, 62, 45);">10\. Checking Details About Containers</span>**

```bash
~/Desktop/Employee-Record-System$ docker inspect frontend
"Networks": {
                "mern": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "f6:2b:38:dd:43:05",
                    "DriverOpts": null,
                    "GwPriority": 0,
                    "NetworkID": "5c8ff14dad46799372c3d8d8236cd19dfdd5b6dc2a1213497553df64fa9e548a",
                    "EndpointID": "7bf53d8bacadaf8f9ce01b0d1efc975dc439859e8c2bb57081c02c67f4b089d0",
                    "Gateway": "172.19.0.1",
                    "IPAddress": "172.19.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DNSNames": [
                        "frontend",
                        "2b121477e774"
                    ]
                }
```

&nbsp;

```bash
~/Desktop/Employee-Record-System$ docker inspect mongodb
 "Networks": {
                "mern": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "ae:98:21:f7:33:61",
                    "DriverOpts": null,
                    "GwPriority": 0,
                    "NetworkID": "5c8ff14dad46799372c3d8d8236cd19dfdd5b6dc2a1213497553df64fa9e548a",
                    "EndpointID": "5858adac8c3bb83ca819ee8f6b2353887de8984a0a2fd4c80358fcb7c234e8a9",
                    "Gateway": "172.19.0.1",
                    "IPAddress": "172.19.0.3",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DNSNames": [
                        "mongodb",
                        "b3b06f6c7540"
                    ]
                }
```

&nbsp;

**<span style="color: rgb(224, 62, 45);">11.</span>**

```bash
~/Desktop/Employee-Record-System/mern$ docker exec -it mongodb mongosh
Current Mongosh Log ID: 69c3c337fcdf25e5fdd805da
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.8.1
Using MongoDB:          8.2.6
Using Mongosh:          2.8.1

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/


To help improve our products, anonymous usage data is collected and sent to MongoDB periodically (https://www.mongodb.com/legal/privacy-policy).
You can opt-out by running the disableTelemetry() command.

------
   The server generated these startup warnings when booting
   2026-03-25T08:32:43.836+00:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
   2026-03-25T08:32:43.838+00:00: For customers running the current memory allocator, we suggest changing the contents of the following sysfsFile
   2026-03-25T08:32:43.838+00:00: We suggest setting the contents of sysfsFile to 0.
   2026-03-25T08:32:43.838+00:00: We suggest setting swappiness to 0 or 1, as swapping can cause performance problems.
------

test> show dbs
admin   40.00 KiB
config  12.00 KiB
local   72.00 KiB
test> use employees
switched to db employees
employees> show collections

employees> exit
```

&nbsp;

**<span style="color: rgb(224, 62, 45);">12\. Build Back-end Image</span>**

```bash
Employee-Record-System/mern/backend$ docker build -t mern-backend .
[+] Building 34.1s (10/10) FINISHED                                                                                                                                               docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                                                                              0.2s
 => => transferring dockerfile: 157B                                                                                                                                                              0.0s
 => [internal] load metadata for docker.io/library/node:18.9.1                                                                                                                                    3.1s
 => [internal] load .dockerignore                                                                                                                                                                 0.1s
 => => transferring context: 2B                                                                                                                                                                   0.0s
 => [1/5] FROM docker.io/library/node:18.9.1@sha256:d6ed353d022f6313aa7c3f3df69f3a216f1c9f8c3374502eb5e6c45088ce68e8                                                                              0.1s
 => => resolve docker.io/library/node:18.9.1@sha256:d6ed353d022f6313aa7c3f3df69f3a216f1c9f8c3374502eb5e6c45088ce68e8                                                                              0.1s
 => [internal] load build context                                                                                                                                                                 0.2s
 => => transferring context: 34.99kB                                                                                                                                                              0.0s
 => CACHED [2/5] WORKDIR /app                                                                                                                                                                     0.0s
 => [3/5] COPY package.json .                                                                                                                                                                     0.1s
 => [4/5] RUN npm install                                                                                                                                                                        25.0s
 => [5/5] COPY . .                                                                                                                                                                                0.3s 
 => exporting to image                                                                                                                                                                            4.3s 
 => => exporting layers                                                                                                                                                                           2.5s 
 => => exporting manifest sha256:e42d2f1f1a0ea06ab8268480690c2be097745cef985c00f209231a668f7943c8                                                                                                 0.1s 
 => => exporting config sha256:bfd217aa26060e02e262fc39c713b3f3ba841a736b7dc298a8bd9395e44f45ce                                                                                                   0.1s 
 => => exporting attestation manifest sha256:caf6777816ab77863e466ebd204c41df620b54e247b4df0b90e5c023550aab22                                                                                     0.1s 
 => => exporting manifest list sha256:8f62852aa8292cb15f0d8730d9cb0d22093be9ac82d8e462b426375aee92da78                                                                                            0.1s
 => => naming to docker.io/library/mern-backend:latest                                                                                                                                            0.0s
 => => unpacking to docker.io/library/mern-backend:latest                                                                                                                                         1.3s

```

&nbsp;

**<span style="color: rgb(224, 62, 45);">13\. Run Backend Container</span>**

```bash
/mern/backend$ docker run --network=mern --name=backend -d -p 5050:5050 mern-backend
47e95108ae816e89a412fee1f5ccb424c3f731c156931dac86217284e05852dc
```

&nbsp;

**<span style="color: rgb(224, 62, 45);">14\. Now Running Front-end, Back-end and Mongodb Container</span>**

```bash
/mern/backend$ docker ps
CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS          PORTS                                             NAMES
47e95108ae81   mern-backend    "docker-entrypoint.s…"   14 minutes ago   Up 14 minutes   0.0.0.0:5050->5050/tcp, [::]:5050->5050/tcp       backend
b3b06f6c7540   mongo:latest    "docker-entrypoint.s…"   47 hours ago     Up 4 hours      0.0.0.0:27017->27017/tcp, [::]:27017->27017/tcp   mongodb
2b121477e774   mern-frontend   "docker-entrypoint.s…"   2 days ago       Up 4 hours      0.0.0.0:5173->5173/tcp, [::]:5173->5173/tcp       frontend
```

![docker1.png](mern/backend/images/docker1.png)

&nbsp;

**<span style="color: rgb(224, 62, 45);">15\. Now we Can See Running Frontend and Backend, DB correctly.</span>**

**<span style="color: rgb(45, 194, 107);">http://localhost:5173/ (check using browser)</span>**

<img src="mern/backend/images/test11.png" alt="test11.png" width="1258" height="337" class="jop-noMdConv">

&nbsp;

![test222.png](mern/backend/images/test222.png)

&nbsp;