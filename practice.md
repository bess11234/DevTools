# Week 2
เพื่อให้สามารถดูข้อมูลการตั้งค่า git ของเราต้องใช้คำสั่ง
```
git config -l
```
เวลาตั้งค่า name กับ email ต้องใช้คำสั่ง
```
git config --global user.name "<name>"
git config --global user.email "<email>"
```
หรือต้องการ **Unset** name กับ email ต้องใช้คำสั่ง
```
git config --global --unset user.name
git config --global --unset user.email
```
เมื่อใช้มีการเพิ่มไฟล์ หรือแก้ไขไฟล์เข้าไป จะทำให้เกิด **Untracked files** โดยสามารถใช้คำสั่งต่อไปนี้ เพื่อดูว่ามีไฟล์ใดที่เป็นแบบนั้น
```
git status
```
แต่ถ้าขึ้น Error แบบนี้
> fatal: not a git repository (or any of the parent directories): .git

แปลว่าเราไม่ได้อยู่ใน git repository และการใช้คำสั่งต่อไปนี้ ก็สามารถทำให้ **repository** -> **git repository**
```
git init
```
## Exercise
โดยให้เราลองสร้าง **Private Repository** ใน Github แล้วนำไป Clone ใส่เครื่อง โดยใช้คำสั่ง
```
git clone <URL>
```
***Hint:***
```
git clone https://username:<Token>@github.com/username/repo.git
```
หรือ
```
git clone https://username:<Token>@<URL ที่เริ่มที่ github.com>
```
Token สามารถสร้างได้ที่ Github โดยต้อง
```
Settings -> Developer settings -> Personal access tokens -> Token (classic) -> Generate new token -> [repo -> admin:repo_hook] -> Generate token
```