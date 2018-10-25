---
title: git使用入门
date: 2018-09-28 02:30:18
tags:
---
## git简介

- 分布式版本控制系统
- 特点：
  - 每个开发者的本地都有一份完整的版本库
  - 开发者可以在不联网的情况下随时随地提交自己的代码到本地仓库
  - 开发者可以在不同的分支上并行开发最后再合并
  - 本地的仓库push到远程仓库（服务器仓库）后开发者可共享远程仓库代码

## git安装

- [参考安装](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000)

## 创建本地库

- 创建一个文件夹
   ```
   mkdir  learngit
   ```
- 进入文件夹
  ```
  cd  learngit
  ```
- 初始化一个git仓库
  ```
  git init
  ```
- 命令截图
![image](http://thumbnail0.baidupcs.com/thumbnail/d413e5fa8af64b72c028ad1b87895429?fid=3825744425-250528-966646351731702&time=1465401600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-AEHxt0R7xwCNTiN5IxS3RqEQUU0%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=3711270336661933697&dp-callid=0&size=c710_u400&quality=100)

 - 没有初始化一个git仓库前用git status查看会提示“not a git repository”是没有master标识的

## 关联远程仓库

- 进入本地的版本库主目录执行
  ```
  git remote -v 
  ```
  ![image](http://thumbnail0.baidupcs.com/thumbnail/89cf7706f8b8e95389f8fb77aa1f0df4?fid=3825744425-250528-563930522901710&time=1465401600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-pBVQjtXuhpERxUTz%2FeR1gWxkx2g%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=3711263226928370562&dp-callid=0&size=c710_u400&quality=100)
  没有提示证明未关联远程仓库

- 将本地库与远程库关联
  ```
  git remote add origin [giturl] 
  ```
- 关联后本地仓库可以将本地的代码push到远程仓库或fetch远程仓库代码到本地实现和其他开发者交换代码
  - 关联后
  ![image](http://thumbnail0.baidupcs.com/thumbnail/befe04447ce2c6ba05519248a9627137?fid=3825744425-250528-600981639792855&time=1465401600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-jNn9vri2Ur1MUXoQdCktzxWsPhw%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=3711256842696586902&dp-callid=0&size=c710_u400&quality=100)
- 从远程仓库克隆到本地也可以实现关联远程仓库
  ```
  git clone [giturl]
  git clone https://username:password@xxxxxx.git
  ```

## git工作区和暂存区

- 工作区（Working Directory）开发者本地可以看到的git目录
- 暂存区（Stage）可以理解为购物车，提交（commit）到本地仓库可以理解为付款
- 工作区暂存区关系
  - ![image](http://thumbnail0.baidupcs.com/thumbnail/f0426bbb9abe83bf55c1cbc2e37572dd?fid=3825744425-250528-475655532752782&time=1465401600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-FSO2DJJAkbdmciIvcYtd8Wc382Q%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=3711247855553088954&dp-callid=0&size=c710_u400&quality=100)
  - 第一步是用git add把修改文件或新增文件（未追踪）添加到暂存区；
  - 第二步是用git commit提交暂存区内容到当前分支(HEAD指针指向的分支)。

## 查看状态
- 查看工作区和暂存区
  ```
  git status
  ```
 - 没有改动的情况下
  
 - 有改动
  
   暂存区改动了feature1.txt文件，工作区改动了README.md文件
- 查看修改内容
  ```
  git diff filename
  ```
  红色的是被改动的文本绿色的是改动后的文本

## 版本回退
 - 查看历史提交记录%h(提交对象的简单哈希值)%s（提交说明）
   ```
   git log --pretty=format:"%h %s" --graph
   ```
 - 回退到对应的提交节点
   ```
   git reset --hard commit_id
   ```

## 远程版本库回退

 - 操作需慎重，因为远程仓库会影响到整个team
 - 删除最后一次提交
 
   1.使用revert历史记录出现放弃的提交记录
    ```
    git revert HEAD
    git push origin master
    ```
   2.使用reset历史记录中不会出现放弃的提交记录
  
    ```
    git reset --hard HEAD^
    git push origin master -f
    ```

## 分支管理
 - 查看本地当前分支
    ```
    git branch
    ```
 - 查看远程库分支
    ```
    git branch –r
    ```
 - 创建分支
    ```
    git branch branchname
    ```
 - 切换分支
    ```
    git checkout branchname
    ```
 - 切换分支后文件目录的变化
 
   检出不同的分支，目录会变化
 - 创建分支前分支结构
   
 - 创建dev分支并切换分支到dev后分支结构
 
 - Dev分支有新的提交后分支结构
 
  
 - 合并分支
   - 查看分支
     ```
     git branch
     ```
   - 合并分支
     ```
     git merge branch-name
     ```
 - 删除本地分支
   ```
   git branch -d <name>
   ```
 - 删除远程分支
   ```
   git branch -r -d origin/branch-name
   git push origin :branch-name
   ```
 - 解决合并冲突 
   - 合并前
   
     ![image](http://thumbnail0.baidupcs.com/thumbnail/ee36dd3fb3b5b3c629764e8e2adc620a?fid=3825744425-250528-1004885273059230&time=1465401600&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-LxDozgxYfTGMsL%2BAHkTOfQ9Ba08%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=3711203702385362080&dp-callid=0&size=c710_u400&quality=100)

   - 执行合并
     ```
     git merge feature1
     ```
   - 查看未合并的冲突文件
     ```
     git status
     ```

   - 根据提示找到未自动合并的文件（unmerged）进行冲突处理
   - 解决冲突后通过下面的命令来标记文件已解决（添加到暂存区）
     ```
     git add unmergedfile
     ```
	 
     ```
     git commit -m "merge detail"
     ```
 - 分支策略
   - master稳定的，仅用来发布新版本
   - develop分支干活
   - 开发人员从develop分支再新开分支干活，完成后再merge回develop分支
  
 - 多人协作
   - 当需要和其他开发者交换代码时，推送（push）代码到远程仓库
     ```
     git push origin branch-name
     ```
   - 推送失败的话证明远程分支比本地更新，需要先拉取（pull) 
     ```
     git pull origin branch-name
     ```
     如果合并有冲突，则解决冲突，并在本地提交。再推送
   - 推送失败还可以先获取（fetch），再对比分支不同，再合并（merge）-建议使用因为它比pull更安全
     ```
     git fetch origin branch-name
     git diff branch-name
     git merge branch-name
     ```
     清除本地与git origin没对应的分支
     git fetch -p
     
## git 生成ssh key

1：生成RSA key 过程 
（1）在指定的用户目录下，右键打开git bash 执行 命名：
```
ssh-agent bash 
```
（2）生成RSA密钥，执行命令：
```
ssh-keygen -t rsa -C lizexian@gridsum.com 
```


## 批量删除分支

```
git branch |grep 'branchName' |xargs git branch -D
```
