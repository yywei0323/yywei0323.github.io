---
layout: post
title: Gits Guild
date: 2022-09-01 20:40:16
description: Build pages by Jekyll + Githubpages
tags: Tools
categories: Environment-Building
giscus_comments: true
featured: true

toc:
    sidebar: left
---

## 1.GIT SSH密钥配置

1. 生成ssh密钥1
   
   ```bash
   ssh-keygen -t ed25519 -C "2286988225@qq.com"
   ```

2. 添加SSH密钥到SSH-Agent
   
   - 启动SSH-Agent
     
     ```bash
     eval "$(ssh-agent -s)"
     ```
   - 添加生成的SSH私钥到SSH-Agent
     
     ```bash
     ssh-add ~/.ssh/id_ed25519
     ```

3. 将SSH公钥添加到Github
   
   - 打印公钥
     
     ```bash
     cat ~/.ssh/id_ed25519.pub
     ```
   - 复制公钥到`Settings > SSH and GPG keys > New SSH key`

4. 验证SSH配置
   
   ```bash
   ssh -T git@github.com
   ```
- 如果成功连接，你将看到类似于以下的输出：
  
  ```bash
  Hi username! You've successfully authenticated, but GitHub does not provide shell access.
  ```
5. 启动SSH配置
   
   ```bash
   Start-Service ssh-agent
   ```

## 2.GIT仓库克隆并提交

1. 克隆仓库 
   
   ```bash
   git clone git@github.com:your_username/your_repository.git
   ```
2. 编辑并提交更改
- 在本地对仓库进行修改。
- 提交更改：
  
  ```bash
  git add .
  git commit -m "Update blog and content"
  ```
3. 将本地更改推送到 GitHub：
- 将本地更改推送到 GitHub：
  
  ```bash
  git push origin master
  ```
- 如果你在 GitHub 上的分支不是 main，请将 main 替换为相应的分支名称。

## 3.GIT仓库自动更新

1. 自动更新仓库的代码，在仓库目录上一级
   
   ```bash
   # autopush.sh
   # 设置项目目录
   cd yywei0323.github.io
   ```

# 获取最新的更改

git pull origin master

# 添加所有更改

git add .

# 提交更改

git commit -m "Auto-update on $(date +'%Y-%m-%d %H:%M:%S')"

# 推送更改到远程仓库

git push origin master

```
2. 新建logfile.log文件并更改autopush.sh的权限

- 因为该代码属于两个用户 因此权限改为chmod 777

```bash
chmod 777 autopush.sh
chmod 777 logfile.log
```

3. 增加自动执行的任务 
- 使用`cron`来定时执行该脚本。首先，编辑`crontab`文件：
  
  ```bash
  crontab -e
  ```
- 添加如下条目来每天定时执行该脚本，例如每天凌晨 2 点执行
  ```bash
  
  ## cron表达式
* * * * * command_to_execute

- - - - -

| | | | |
| | | | ----- 星期几 (0 - 7) (0 或 7 表示周日)
| | | ------- 月份 (1 - 12)
| | --------- 日期 (1 - 31)
| ----------- 小时 (0 - 23)
------------- 分钟 (0 - 59)

0 2 * * * bash /xx/blog/autopush.sh >> /xx/blog/logfile.log 2>&1

```
    - 0 2 * * * 表示每天凌晨 2:00 执行任务。
    - bash /opt/sharedVolumes/yangyuwei/blog/autopush.sh >> /opt/sharedVolumes/yangyuwei/blog/logfile.log 2>&1 将日志输出重定向到文件。需要确保该命令在用户下可以使用。
```

4. 权限问题
- 由于该代码库是由jupyter notebook中yangyuwei用户编写 由root用户上传的；因此这里需要两个用户建立用户组，两个用户共享权限；
- 新建用户组->将用户增加到用户组内->修改权限

```bash
##新建用户组
sudo groupadd bloggroup
##增加用户数目
sudo usermod -aG bloggroup root
sudo usermod -aG bloggroup yangyuwei
##修改权限
sudo chown -R yangyuwei:bloggroup /xx/blog
```
