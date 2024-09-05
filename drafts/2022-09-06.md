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
1. 生成ssh密钥
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
git push origin main
```
- 如果你在 GitHub 上的分支不是 main，请将 main 替换为相应的分支名称。