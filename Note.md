# Week 1
เพื่อให้สามารถดูข้อมูลการตั้งค่า git ของเราต้องใช้คำสั่ง
```bash
git config -l
```
เวลาตั้งค่า name กับ email ต้องใช้คำสั่ง
```bash
git config --global user.name "<name>"
git config --global user.email "<email>"
```
หรือต้องการ **Unset** name กับ email ต้องใช้คำสั่ง
```bash
git config --global --unset user.name
git config --global --unset user.email
```
เมื่อใช้มีการเพิ่มไฟล์ จะทำให้เกิด **Untracked files** หรือแก้ไขไฟล์เข้าไป จะทำให้เกิด **Changes not staged for commit** โดยสามารถใช้คำสั่งต่อไปนี้ เพื่อดูว่ามีไฟล์ใดที่เป็นแบบนั้น
```bash
git status
```
![PNG](./images/1.png)

![PNG](./images/2.png)

แต่ถ้าขึ้น Error แบบนี้

`fatal: not a git repository (or any of the parent directories): .git`

แปลว่าเราไม่ได้อยู่ใน git repository และการใช้คำสั่งต่อไปนี้ ก็สามารถทำให้ **repository** -> **git repository**
```bash
git init
```
## Exercise
โดยให้เราลองสร้าง **Private Repository** ใน Github แล้วนำไป Clone ใส่เครื่อง โดยใช้คำสั่ง
```bash
git clone <URL> <Optional:FolderName>
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
ใช้คำสั่ง git add เพื่อเปลี่ยนสถานะจาก **Untracked files** เป็น **Changes to be committed**
```bash
git add <all_files>
```
หรือต้องการ Commit ไฟล์ทุกไฟล์
```bash
git add .
```
เมื่อต้องการ Commit ลง github ให้ใช้คำสั่ง
```bash
git commit -m "Example"
```
`git commit` จะสร้างจุด Checkpoint ทำให้ย้อนเวลาได้

ถ้าต้องการย้าย Branch ไป Branch ที่ต้องการ
```bash
git branch -M <branch>
```
ถ้าต้องการเชื่อม git เข้ากับ git init ต้องใช้คำสั่ง
```bash
git remote add origin <REMOTE-URL>
git remote add <name> <REMOTE-URL> # เปลี่ยน Branch นอกจาก origin ได้
```
ุถ้าต้องการเปลี่ยนชื่อ git repository ให้เป็นชื่ออื่นให้ใช้คำสั่ง
```bash
git remote rename <name-origin> <new-name>
```

ถ้าต้องการลบ URL ของ repository นั้น ๆ ให้ใช้คำสั่ง
```bash
git remote remove <name>
git remote remove origin
```

ถ้าต้องการอัพขึ้นไปยัง git ต้องใช้คำสั่ง
```bash
git push -u origin <branch> # -u จะทำให้ track branch ให้สามารถ git pull ได้เลย โดยจะเอาตามที่เคย git push -u ไป
git push origin <branch> # ทำให้ git pull ต้องเลือก branch
```
โดยเมื่อต้องการอัพไฟล์เข้าไปยัง git repository ที่ได้สร้างขึ้นใหม่ใน github ให้ใช้คำสั่งดังนี้
```bash
git branch -M <branch>
git remote add origin <Remote-URL>
git push -u origin <branch>
```
> โดย branch ต้องมีชื่อเดียวกันกับตอน push
```bash
git branch -M test
git push -u origin test
```

เมื่อต้องการดึงข้อมูลจากใน **git repository** เพื่อทำการอัพเดทข้อมูลภายใน **local repository** โดยจะยังไม่ได้อัพเดททันทีแต่จะนำ Commit ล่าสุดเข้ามารอที่เครื่อง ใช้คำสั่ง
```bash
git fetch
```
เมื่อต้องการให้อัพเดทข้อมูลไปยัง **Working Directory** จากที่ได้ดึงข้อมูลมาจากการใช้ `git fetch` ให้ใช้คำสั่ง
```bash
git merge
```
หรือ เมื่อดึงเสร็จเราสามารถอัพเดท **local repository** ให้ตรงกับ Commit ล่าสุดให้ใช้คำสั่งนี้ หรือจริง ๆ สามารถใช้คำสั่งนี้เพื่อดึงข้อมูล Commit ได้เลยไม่ต้อง `git fetch + git merge`
```bash
git pull
```
เมื่อต้องการดู Commit ที่ได้ทำไปให้ใช้คำสั่ง
```bash
git log
```
เมื่อต้องการย้อนกลับไป ให้ข้อมูลเหมือน git repository ที่ remote อยู่ให้ใช้
```bash
git checkout <branch>
git checkout origin/main
```

# Week 3
