# Week 1 (GITHUB)
เพื่อให้สามารถดูข้อมูลการตั้งค่า git ของเราต้องใช้คำสั่ง
```bash
git config -l
```
เวลาตั้งค่า name กับ email ต้องใช้คำสั่ง
```bash
git config --global user.name "<name>"
git config --global user.email "<email>"
git config --global credential.username "<username>"
```
หรือต้องการ **Unset** name กับ email ต้องใช้คำสั่ง
```bash
git config --global --unset user.name
git config --global --unset user.email
```
เมื่อมีการเพิ่มไฟล์ (ไม่ใช่อัพเดท) จะทำให้เกิด `Untracked files` หากแก้ไขข้อมูลไฟล์ จะทำให้เกิด `Changes not staged for commit` แทน โดยสามารถใช้คำสั่งต่อไปนี้ เพื่อดูว่ามีไฟล์ใดที่เป็นแบบนั้น
```bash
git status
```

![CREATE FILE](./images/2.png)

![UPDATE FILE](./images/1.png)

แต่ถ้าขึ้น Error แบบนี้

`fatal: not a git repository (or any of the parent directories): .git`

แปลว่าเราไม่ได้อยู่ใน git repository และการใช้คำสั่งต่อไปนี้ ก็สามารถทำให้ `repository` -> `git/remote repository`
```bash
git init
```

เราสามารถสร้างไฟล์ `.gitignore` เพื่อให้ชื่อไฟล์ที่อยู่ในนี้ ไม่อัพขึ้น git สามารถใช้เว็บ
[gitignore](https://www.toptal.com/developers/gitignore) เพื่อ Generate `.gitignore` ได้

## Exercise
โดยให้เราลองสร้าง `Private repository` ใน Github แล้วนำไป Clone ใส่เครื่อง โดยใช้คำสั่ง
```bash
git clone <URL> <Optional:FolderName>
git clone -b <branch> <URL> <Optional:FolderName> # เมื่อสร้างขึ้นมาแล้วจะยัดใส่ branch ที่เรากำหนด
```
***Hint:***
```bash
git clone https://username:<Token>@github.com/username/repo.git <Optional:FolderName>
```
หรือ
```bash
git clone https://username:<Token>@<URL ที่เริ่มที่ github.com> <Optional:FolderName>
```
Token สามารถสร้างได้ที่ Github โดยต้อง
```bash
Settings -> Developer settings -> Personal access tokens -> Token (classic) -> Generate new token -> [repo -> admin:repo_hook] -> Generate token
```

# Week 2
ใช้คำสั่ง `git add` เพื่อเปลี่ยนสถานะจาก `Untracked files && Changes not staged for commit` เป็น `Changes to be committed`

เปลี่ยนจาก state `Working directory` -> `Staging Area`
```bash
git add <file file ...>
```
หรือต้องการ Commit ไฟล์ทุกไฟล์
```bash
git add .
```
เมื่อต้องการ Commit ลง github ให้ใช้คำสั่ง

เปลี่ยนจาก state `Staging Area` -> `Local repository`
```bash
git commit -m "Example"
```
`git commit` จะสร้างจุด Checkpoint ทำให้ย้อนเวลาได้

ถ้าต้องการย้าย Branch ไป Branch ที่ต้องการ
```bash
git switch <branch>
git checkout <branch>
```

ถ้าต้องการเชื่อม git เข้ากับ git init ต้องใช้คำสั่ง
```python
git remote add origin <REMOTE-URL>
git remote add <name> <REMOTE-URL> # กำหนดชื่อแทน url นอกจาก origin ได้
```
ถ้าต้องการเปลี่ยนชื่อ git repository ให้เป็นชื่ออื่นให้ใช้คำสั่ง
```bash
git remote rename <name-origin> <new-name>
```

ถ้าต้องการลบ URL ของ repository นั้น ๆ ให้ใช้คำสั่ง
```bash
git remote remove <name>
git remote remove origin
```

ถ้าต้องการดูว่าแต่ละ `remote <name>` ชื่ออะไรให้ใช้
```bash
git remote -v
```

ถ้าต้องการอัพขึ้นไปยัง git ต้องใช้คำสั่ง
ทำให้ข้อมูลใน state `Local repository` -> `Git/Remote repository`
```python
git push -u <name-origin/..> <branch> # -u จะทำให้ track branch ให้สามารถ git pull/git push ได้เลย โดยจะเอาตามที่เคย git push -u ไป
git push <name-origin/..> <branch> # ทำให้ git pull/git push ต้องเลือก branch
```
โดยเมื่อต้องการอัพไฟล์เข้าไปยัง git repository ที่ได้สร้างขึ้นใหม่ใน github ให้ใช้คำสั่งดังนี้
```py
git branch -M <branch> # เปลี่ยนชื่อ branch ปัจจุบัน โดย Default master
git remote add <name-origin/...> <Remote-URL> # กำหนด Url ว่าจะเชื่อมกับ Remote repository ที่ไหน
git push -u <name-origin/...> <branch> # เมื่อทำการ add และ commit แล้วใช้คำสั่งนี้จะอัพโหลดขึ้น Remote repository ที่ใช้เข้าไปหากมี -u จะ track ตามด้วย
```
โดย branch ที่จะ push เข้าไป ต้องมีอยู่ใน `Local repository`
```py
git branch # เพื่อดู branch ทั้งหมด
git push -u <name-origin/...> <branch>
```

เมื่อต้องการดึงข้อมูลจากใน `Git/Remote repository` เพื่อทำการอัพเดทข้อมูลภายใน `Local repository` โดยจะยังไม่ได้อัพเดททันทีแต่จะนำ Commit ล่าสุดเข้ามารอที่เครื่อง ใช้คำสั่ง

`Git/Remote repository` -> `Local repository`
```bash
git fetch <name-origin/...> <branch>
```
เมื่อต้องการให้อัพเดทข้อมูลไปยัง `Working directory` จากที่ได้ดึงข้อมูลมาจากการใช้ `git fetch` ให้ใช้คำสั่ง

`Git/Remote repository` -> `Working directory`
```bash
git merge
git merge origin/main
```
หรือ เมื่อดึงเสร็จเราสามารถอัพเดท `Local repository` ให้ตรงกับ Commit ล่าสุดให้ใช้คำสั่งนี้ หรือจริง ๆ สามารถใช้คำสั่งนี้เพื่อดึงข้อมูล Commit ได้เลยไม่ต้อง `git fetch + git merge`
```bash
git pull <name-origin/...> <branch>
```
เมื่อต้องการดู Commit ที่ได้ทำไปให้ใช้คำสั่ง
```bash
git log
```
เมื่อต้องการย้อนกลับไป ให้ข้อมูลเหมือน git repository ที่ remote อยู่ให้ใช้ หรือไปที่ branch นั้น ๆ สามารถใช้ได้โดย
- ย้อนเวลาผ่าน COMMIT-HASH
- ย้ายไป branch ที่ต้องการ
```python
git checkout <branch>
git checkout origin/main # last commit
git checkout [COMMIT-HASH] # git log --oneline แสดง COMMIT-HASH ที่อยู่บน git/remote repository
```

![Stage](./00_GIT/Week02/images/staged.PNG)

## Extras
เมื่อต้องการหาความแตกต่างของไฟล์ว่าเราได้แก้อะไรไปบ้าง
โดยคำสั่งนี้หากไม่มีการใช้ Flaged เพิ่มเติมจะหาความแตกต่างระหว่างไฟล์ใน `Working directory` <-> `Staging Area`
```bash
git diff
```

หากต้องการหาความแตกต่างระหว่าง `Staging Area` <-> `Local repository` ให้ใช้
```bash
git diff --staged | --cached
```

หากสิ่งที่เราแก้ไปมีการแก้ Format แล้วเกิด Whitespace แล้วเราไม่ต้องการสนใจมันให้ใช้
```bash
git diff -w
```
# Week 3

วิธีเช็คว่า Git repository มี branch อะไรบ้าง และดูได้ว่าเราอยู่ branch
```bash
git branch
```
และสามารถใช้เพื่อเพิ่ม branch ได้อีกด้วย
```bash
git branch <new_branch>
```
วิธีการเปลี่ยนชื่อ
1. `git branch -m/-M <rename_branch>` จะเปลี่ยนชื่อ branch ที่ HEAD ชี้อยู่ (ที่เราอยู่ปัจจุบัน)
2. `git branch -m/-M <branch> <rename_branch>` จะเปลี่ยนชื่อ branch ที่เรากำหนด

เมื่อต้องการดูว่า `Local repository` เราได้อัพขึ้น branch ไหนใน `Git/Remote repository` ให้ใช้
```bash
git branch -r
```
เมื่อต้องการดู Last commit แต่ละ branch
```bash
git branch -v
```

และเมื่อต้องการเปลี่ยน branch ไปอีกอันให้ใช้ คล้าย `git checkout <branch>`
```bash
git switch <branch>
```

เมื่อต้องการลบ branch ออกให้ใช้
```python
git branch -d <branch> # มีการเตือน หากยังไม่ทำการ Merge เข้ากับตัวหลัก
git branch -D <branch> # ลบทันที
```
> ``🔥`` ไม่สามารถลบ branch ได้หากเราอยู่ใน branch นั้น ๆ

เมื่อต้องการสร้าง branch แล้วเข้าไปยัง branch นั้นทันที
```bash
git checkout -b <new_branch>
git switch -c/-C <new_branch>
```

เมื่อต้องการ merge กับ branch อื่น ๆ ไปยัง branch ของเราให้ใช้
```python
git merge <branch> # อยู่ที่ว่าปัจจุบันเราอยู่ branch อะไร โดยจะ merge เข้ากับ branch ที่ใส่เข้าไป
```

## Extra
หาก pull แล้วเกิด conflict เกิดขึ้น ให้ทำการ merge เมื่อ merge เสร็จแล้วห้ามลืม
```
git commit -m "Merge"
```

หาก merge กับ branch เสร็จแล้วต้องการลบ branch ให้ใช้
```bash
git branch -d/-D <branch>
```
แต่ใน `Git/Remote repository` ยังไม่ได้ลบให้ใช้คำสั่ง
```py
git push -d <name-origin> <branch> # ต้องระบุ <name> <branch> เสมอ ใช้ tracked ไม่ได้
```

# Week 4

เมื่อต้องการ Update ไฟล์ทั้งหมดที่ถูกแก้ไข โดยไม่ต้อง `add` และ commit เลยให้ใช้ `-am`

หรือก็คือไฟล์ที่มีสถานะเป็น `Changes not staged for commit`
```bash
git commit -am "<text>"
```
> ``🔥`` ไม่สามารถใช้กับไฟล์ที่เพิ่งสร้างได้

`git commit -a` เป็นการระบุ File ที่ต้องการ Commit

เมื่อต้องการกู้คืนข้อมูลจากการที่เรา Commit ไปแล้วให้ใช้ tree หรือ HEAD คล้ายการทำ Ctrl+Z เลข 0, 1, 2, 3.. คือจำนวนครั้งที่ย้อนไป
- ใช้งานได้จากการที่ยังไม่ Commit เมื่อต้องการรีไฟล์ที่ต้องการ
```python
git restore --source=<HEAD/tree>[~(1,2,3..)] <file, file, ...>
git restore -s <HEAD/tree>[~(1, 2, 3)] <file, file, ...>
git restore -s <HEAD/tree>[~(1, 2, 3)] . # ทุกไฟล์
```

เมื่อเผลอกด commit ไฟล์ หรือไม่ได้ต้องการให้ไฟล์บางไฟล์ commit ให้ใช้ จะเป็นการย้อน staged กลับไปยังก่อน add
- อาจจะใช้ตอนที่ `git add .` แล้วมีไฟล์ที่ไม่ต้องการ commit เลยใช้คำสั่งนี้
```python
git restore --staged <file, file, ...>
git restore -S <file, file, ...>
git restore -S . # ทุกไฟล์
```

เมื่อต้องการรีเซ็ต `soft` กลับไปยัง commit ที่ต้องการ โดยไม่มีผลกระทบต่อเนื้อหาในไฟล์ 
- เมื่อไปดูที่คำสั่ง `git log --oneline` ก็จะกลับไปยัง commit ที่ใส่ HASH เข้าไป
- จะเห็นว่า `git log --oneline` จะมี commit ที่เราเลือกเป็น commit ล่าสุด
```bash
git reset --soft <COMMIT-HASH>
git reset <COMMIT-HASH>
```
> ``🔥`` ไฟล์ยังสามารถ commit ได้ต่อ เพราะเมื่อย้อนไปเนื้อหาไม่ถูกกระทบ ทำให้ต่างกับใน git repository ไฟล์นั้น ๆ เลยอยู่ใน Stage ที่รอการ commit

เมื่อต้องการรีเซ็ต `hard` กลับไปยัง commit พร้อมกับเนื้อหาไฟล์ของ commit นั้น
- จะเห็นว่า `git log --oneline` จะมี commit ที่เราเลือกเป็น commit ล่าสุด
```bash
git reset --hard <COMMIT-HASH>
```
> ``🔥`` การย้อนแบบนี้ไม่มีผลต่อไฟล์ที่พึ่งสร้าง และยังไม่ได้ถูก Commit

เมื่อต้องการ revert กลับไปยัง commit ก่อน และแก้ไขข้อมูลในไฟล์เอง เมื่อมีการ revert แล้วจะให้แก้ conflict กับ commit หลังมัน และจะเกิด commit ใหม่ให้มาด้วย
```python
git revert <COMMIT-HASH>
# กดเสร็จจะมีการ conflict ของไฟล์ให้แก้ไข
git add .
git revert --continue # จะมีขึ้น vim แก้ไขชื่อของ Commit :wq | :!q
git log --oneline # จะมีการเพิ่มขึ้นของ Commit
```
# Week 5 (GOOGLE CLOUD)

การสร้าง Key ที่ใช้ในการ Authentication เข้าไปใน Instance ที่มี Public key ของเรา
```bash
mkdir mykey
cd mykey
ssh-keygen -t rsa -b 2048 -C "username" -f  username_gcp_key # Generate RSA KEY
ssh -i ./username_gcp_key username@[EXTERNAL_IP] # ./username_gcp_key เป็น Private key # username@[EXTERNAL_ID username เป็นของ Instance
```

# ข้อสอบกลางภาค
70 ข้อ (35 คะแนน ข้อกา) 2 ข้อ 1 คะแนน
- github 57
- google cloud 3
- docker ออกครึ่งเดียว 10

# Week 6
## Generate RSA Key
```python
ssh-keygen -t rsa -b 2048 -C "username" -f filename_key
```
> ``🔥`` จะได้ไฟล์ .pub ซึ่งเก็บ Public key ไว้ และไฟล์ที่ไม่มีนามสกุลเก็บ Private key

## SSH TO INSTANCE
โดยเราต้องกำหนด `Public key` ให้ Instance รู้ก่อนจึงใช้ `Private key` ของเราเข้าผ่าน ssh ได้
```
ssh -i <PathPrivateKey> <usernameINinstance>@[EXTERNAL_IP]
```

# Week 7
## kill signal
```python
ps -a # ดู Signal
kill -9 <Signal>
```

## Delete all containers
```
docker stop $(docker ps -a -q)  
docker rm $(docker ps -a -q) 
docker rmi $(docker images -q) 
docker volume rm $(docker volume ls -q)  
docker network prune -f
```

## Nginx
```python
docker run nginx # ถ้าไม่มี Nginx จะโหลด และจะสร้าง Container Nginx ขึ้นมา ถ้ามี Nginx จะสร้าง Container อีกตัวขึ้นมา
```

## BusyBox
```python
docker run busybox hi there # เหมือน Nginx
```

## Ubuntu
```python
docker run ubuntu
docker run ubuntu sleep 5
docker run ubuntu sh -c "echo 'Hello' && echo 'World' && echo `pwd`"
```

## Docker
- สามารถกำหนด RAM หรือสเปคที่ให้ Container แต่ละอันใช้ได้

## Docker vs Virtual Machine
- Virtual Machine
    - หนักกว่า (GB)
    - ใช้งานได้เยอะกว่า
    - มีการ Boot up หลายอย่าง
- Docker
    - เบากว่า (MB)
    - ใช้งานได้น้อยกว่า
    - Boot up น้อย

ง่าย ๆ คือ Docker เล็ก เร็ว มีประสิทธิภาพ แต่การใช้งานจำกัด Virtual Machine ตรงกันข้าม

Docker daemon คือตัวจัดการให้ภายในเครื่องเราเมื่อมีการดึงข้อมูลจาก Registry จะดูว่าข้อมูลเราตรงไหม

Dockerfile คือ File ที่กำหนดคำสั่ง หรือ Image ในการสร้าง Docker Image ก็คือเอาไว้ Custom image นั้นแหละ

## Command
Run container
```bash
docker run nginx
docker run --cidfile <id-cotainer> <image>
```
Run test
```bash
docker run busybox echo hi there
```
> ``🔥`` busybox เป็น Image ขนาดเล็กที่เหมือน Ubuntu แต่เล็กกว่าไว้ใช้ทดสอบ

Run ubuntu
```python
docker run ubuntu
docker run ubuntu sleep 5 # ให้หลับ 5 วิ
docker run ubuntu sh -c "echo 'Hello' && echo 'World' && ls && pwd && date"
```

## Port Mapping
คือการทำ Port ออกข้างนอก เข้าข้างในได้
```python
docker run -p 80:5000 myname/simple-app # 80 ข้างนอก 5000 ข้างใน โดยคนข้างนอกเข้ามาต้องใช้ Port 80

docker run -p 3306:3306 mysql
# ข้างนอก (ตัวแรก) Port เดียวกันไม่ได้
# ข้างใน (ตัวสอง) Port เดียวกันได้

docker run mysql # ไม่ให้ออกข้างนอก
docker run -d <service> # รัน Service โดยให้เป็น backgroud process
```

## Volumn Mapping
```python
docker run –v /opt/datadir:/var/lib/mysql mysql # : เอาไว้คั่นระหว่างตัวที่จะ Link กัน
docker run -d -p 8083:80 -v ${PWD}/web_demo:/usr/share/nginx/html:ro nginx
```

# Week 8
## Stop Containers
```python
docker ps
docker stop <Names> # Names ของ Container เปลี่ยน Status เป็น Exited (0)
docker stop ($docker ps -aq) # หยุด Containers ทั้งหมด
```

## Remove Containers
```python
docker ps
docker rm <Names> # ลบ Containers
docker rm ($docker ps -aq) # ลบ Containers ทั้งหมด
docker container prune -f # ลบ Containers ที่มี Status Exited (0) หรือก็คือหยุด
```

## Images Container
```python
docker images # ดู Images ทั้งหมดใน Docker
```

## Images Remove
```python
docker rmi <image_repository> # ดู repository ได้จาก `docker images`
docker rmi -f $(docker images -aq) # ลบ Image ทั้งหมด
docker rmi prune -f # ลบ Image ที่ไม่ได้ใช้
```

## Docker command
```python
docker pull <image> # image อย่าง ubuntu
docker build -t <nameOFimage> <pathtoDockerfile> # สร้าง Images ผ่าน Dockerfile
docker run -it <image> [<command_exec[sh, bash, /bin/bash, zsh, ..]>]
docker run <image> # Create container from images and run on current process
docker run -d <image> # Create container from images and run on backgroud process
docker ps -a # Show containers
docker exec <container_name> <run_command> # อย่าง Container_name นั้นมี Image เป็น Ubuntu; run_command คือคำสั่งที่จะรันใน container นั้น โดย status ต้องเป็น UP
docker inspect <cotainer_name> # ส่อง Container นั้น ๆ ว่ามี IP, Name, State, Path
docker logs <container_name> # ส่อง Container ว่าใช้ Command Line อะไรบ้าง และเกิดผลลัพท์อะไร
```

## Docker set environment variable
ยกตัวอย่าง Python
```py
# app.py
os.environ['APP_COLOR']

# cmd docker
docker run -p 8081:8081 -d --name container_red -e APP_COLOR=red flask-docker-app
```
> ``🔥`` โดยที่ -e จะเป็นการกำหนด Environment variable

## Status codes and HTTP methods
HTTP Methods
- GET   : retrive an existing resource (read only)
- POST  : create a new resource/send information
- PUT   : update an existing resource
- PATCH : partically update an existing resoure
- DELETE: delete a resource

HTTP status code
- 2xx   : successful
- 3xx   : redirect
- 4xx   : client error
- 5xx   : server error

## Dockerfile
```
RUN # ทำคำสั่งหลัง Build
CMD # ทำคำสั่งหลัง Run Build เสร็จ
```

## Tips
```python
เมื่อมีการรันไฟล์ Container ที่ Image มี Dockerfile ควรดู Port ที่เขียนไว้ด้วย เพราะเมื่อทำการ docker run -p <อะไรก็ได้>:<ตาม Dockerfile>
```

# Week 10
เราสามารถใช้คำสั่ง
```py
docker restart <container> # ใช้เพื่อทำการรี Container
docker network # Bride (Default), None สร้าง Network เพื่อสร้าง Connection กับ Container
docker run --network <network> # ใช้เพื่อสร้าง Container และ Assign network
```

## Tips
- หากมี Port ที่ใช้ไม่ได้ให้ลองไปดูที่ Firewall ว่ามีการอนุมัติ Port หรือยัง

# Week 11
## Dockerfile
```py
FROM <image:tag> # เซ็ต Base Image สำหรับ Container
COPY . /test/  # จะ Copy Folder ทั้งหมดใส่ไปยัง Container
LABEL <key>=<value> # เพิ่ม Metadata ไปยัง Image
WORKDIR /test # จะเข้าไปยัง Folder ที่เราระบุ
RUN npm install # เป็น Command สั่งรันโปรแกรม
ENV VERSION 1.0 # เซ็ต Environment variable
VOLUME ['/data'] # Map volume
ENTRYPOINT <command> <param1> <param2> # กำหนดคำสั่งเริ่มต้น RUN Command ที่ตั้งไว้ โดยต้องเป็นคำสั่งที่ Executable
EXPOSE 8081 # เปิด PORT
CMD ['node', '/nodejs/main.js'] # รัน Command หลังสร้าง Container เสร็จ ครั้งเดียว
```

## Login Dockerhub
```
docker login -u <username>
<password/access token>
```

### Deploy Private Registry
ใช้หลัง Login แล้ว
```
docker build -t <your_username>/<image_repository_name>:tag .
docker push <your_username>/<image_repository_name>:tag
docker pull <your_username>/<image_repository_name>:tag
```

## Docker networks
ประเภทของ Networks มี 3 ประเภท
1. Bridge - `docker run ubuntu`
2. None - `docker run ubuntu --network=none`
3. Host - `docker run ubuntu --network=host`

### List network
```
docker network ls
```

เมื่อทำการ Inspect จะได้ข้อมูล network ด้วย
```py
docker inspect <container
....
"Networks": {
    "bridge": {
        "Gateway": "127.2.2.2" # มั่ว
        "IPaddress": "127.2.2.2" # มั่ว
        "MacAddress": "127.2.2.2" # มั่ว
    }
}
```
หากไม่ได้อยู่ Network เดียวกัน Container จะสื่อสารกันไม่ได้ โดย Docker จะมี Embedded DNS ให้ทำให้คุยกันได้
![alt text](./images/3.png)

## Docker compose
แทนที่จะรัน Docker container ทีละอันเราสามารถเขียนไฟล์ชื่อ `docker-compose.yml`
```yml
version: '3'
service:
    web:
        image: "yourname/simple-webapp"
    database:
        image: "mongodb"
    messaging:
        image: "redis:alpine"
    orchestration:
        image: "ansible"
```
โดยใช้คำสั่ง
```py
docker compose up
```
ทำงานเดียวกันกับคำสั่งดังต่อไปนี้
```
docker run yourname/simple-webapp
docker run mongodb
docker run redis:alpine
docker run ansible
```
### docker compose link
เป็นการ Map เชื่อม Container กับ Container
```yaml
version: '3'
redis:
    image: redis
db:
    image: postgres:9.4
vote:
    image: voting-app
    ports:
        - 5000:80
    links:
        - redis
result:
    image: result-app
    ports:
        - 5001:80
    links:
        - db
worker:
    image: worker
    links:
        - redis
        - db
```

### docker compose build
หากต้องการให้เกิดการ Build image เรื่อย ๆ
```yaml
version: '3'
redis:
    image: redis
db:
    image: postgres:9.4
vote:
    build: ./vote
    ports:
        - 5000:80
    links:
        - redis
result:
    build: ./result
    ports:
        - 5001:80
    links:
        - db
worker:
    build: ./worker
    links:
        - redis
        - db
```

### docker compose networks
```yaml
version: '3'
services:
    redis:
        image: redis
        networks:
            - back-end
    db:
        image: postgres:9.4
        networks:
            - back-end
    vote:
        image: voting-app
        networks:
            - front-end
            - back-end
    result:
        image: result
        networks:
            - front-end
            - back-end
networks:
    front-end:
    back-end:
```

## Lab
เมื่อต้องการสร้าง Image จาก Dockerfile ที่ไม่ได้ชื่อ Dockerfile ให้ใช้คำสั่ง
```py
docker build -t <image_name> -f <name_Dockerfile> <pathToDockerfile>
```
### Lab 0
```Docker
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Hello from both CMD and ENTRYPOINT!"]
```
```py
docker build -t cmd-entrypoint-example -f Dockerfile-CMD-ENTRYPOINT .
docker run cmd-entrypoint-example "Custom message with both CMD and ENTRYPOINT"
```
จะเห็นว่า
- CMD สามารถโดนใส่ทับได้หากเราใส่ Argument
- Entrypoint จะไม่โดนทับหากมี Argument
- Entrypoint คำสั่งจะอยู่เสมอหากใส่ Argument อะไรไปจะเข้าไปคำสั่งนั้น ต.ย echo
### Lab 2
เมื่อต้องการ Copy image และแก้ชื่อกับ Tag ทำเพื่อให้สร้าง Push เข้า Registry ได้ (Dockerhub) โดยต้องมีรูปแบบ `<username>/<image:tag>`
```
docker tag <image:tag> <new:tag>
docker tag <image:tag> <username>/<image:tag>
```

### Lab 3
เมื่อต้องการดู Network
```
docker network ls
```
เมื่อต้องการดูข้อมูลภายใน Network
```
docker network create --subnet <IPADDRESS/16> <name>
docker network inspect <name>
```
หากต้องการให้ Connect/Disconnect container เข้ากับ network ใช้
```
docker network connect <network_name> <container_name>
docker network disconnect <network_name> <container_name>
```
หากต้องการลบ Network ให้ทำโดย
```py
docker network rm <name> # หากไม่ได้ หมายความว่าต้องทำการ disconnect ทุก Container ที่เชื่อมอยู่ออกก่อน
```
- หากต้องการให้ Container สื่อสารกันได้ต้อง Connect ที่ Network เดียวกัน

### Lab 4
โดยจะมีการให้ทำ Compose up หากทำแล้วจะเกิดการสร้าง Image และ Container
```
docker compose up
```
และเมื่อใช้คำสั่ง Compose down จะทำการลบ Container ให้อัตโนมัติ แต่ Network, Image ยังอยู่เพื่อให้รันได้เร็วขึ้นในการทำ Compose up อีก
```
docker compose down 
```
หากต้องการลบ Container, Network, Image ให้ใช้
```
docker compose down --rmi all --volumes --remove-orphans
```
และหากต้องการลบ Network/Volume ที่ไม่ได้ใช้ให้ใช้คำสั่ง
```py
docker network prune
docker volume prune
```

### Lab 5
เมื่อทำเสร็จ Compose เสร็จแล้วจะทำให้เราสามารถ Deploy เข้า Kubernetes ได้

# Week 12
- เมื่อทำ `docker compose up` จะมีการเช็คไฟล์ .env ให้อยู่แล้ว
- เมื่อเราต้องการให้เป็น Backgroud process ต้องใช้คำสั่ง `docker compose up -d`

# Week 13
DevOpv เป็นอาชีพที่ทำทั้ง Deveplop และ Operation โดยจะทำทั้ง Development และ Deployment
- ทุกอย่างเป็นแบบ Automate project
- Deploy เรื่อย ๆ แทนการ Deploy ทีเดียวใหญ่ ๆ
- Rome ค่อย ๆ สร้าง

## DevOps Phase
![alt text](./images/week12_1.png)

CI (Continuous Intregration)
CD มีสองความหมาย (ออกสอบ)
- Continuous Delivery -- Maunal Approval
- COntinuous Deployment

## DevOps Tools
![alt text](./images/week12_2.png)

## CI/CD
![alt text](./images/week12_3.png)
- CI เป็นการรวมโค้ด
- CD เป็นการส่งทำ Test และ Deploy (ส่วนใหญ่เริ่มใช้โปรแกรม Tools ไม่ค่อยใช้คนแล้ว)

## INSTALL Jenkins
```py
sudo apt-get update # อัพเดท System
# Jenkins ใช้ JAVA เลยต้องลง
sudo apt update
sudo apt install -y fontconfig openjdk-17-jre
java -version
# Install Jenkins (Long-term support release)
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

## START Jenkins
```py
# เปิด Service Jenkins เมื่อเปิดแล้วมันจะอยู่ที่ Port 8080
sudo systemctl enable jenkins
sudo systemctl start jenkins
# (ต้องทำ)
sudo usermod -a -G docker jenkins # ใส่กลุ่ม docker ให้ jenkins
sudo usermod -a -G docker $USER # ใส่กลุ่ม docker ให้ user
```
### GET ADMIN PASSWORD
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
### Localhost
สามารถเข้า Service ได้ที่ Port 8080

### First Jenkins Pipeline
```py
pipeline {
    agent any  // Execute on any available Jenkins agent # ใครจะรันก็ได้

    stages {
        stage('Hello World') {
            steps {
                sh  'echo Hello World!'
            }
        }
    }
}
```
### PERMISSION DENIED
หากเกิดขึ้นต้องลอง `sudo reboot` แล้วรอเวลาให้ Instance reboot
![alt text](./images/week12_4.png)

### Authenticate Jenkins
```py
Username: bess11234
Password: Ab123456*
```

# Week 14
## WITH SCM
๋JUNKINS_FILE อยู่ใน github โดยจะง่ายกว่าหาก Project ที่ต้องทำนั้นใหญ่

## WITHOUT SCM
JUNKINS_FILE อยู่ใน JENKINS เอง
![alt text](./images/13.png)

## NEED github COMMUNICATE TO dockerhub
ต้องตั้งค่า Webhook โดย Jenkins จะมีการตรวจว่า github มีการ push หรือป่าว หากมีจะทำการ build ให้เอง ไม่ต้องกด build now