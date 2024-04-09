---
title: 提交代码到github
description: 记录在mac 环境配置并提交代码到github
author: cotes
date: 2024-03-30 18:19:00 +0800
categories: [工具, git]
tags: [git]
render_with_liquid: false
---
## 1、安装git并配置个人信息
- mac 上自带git 工具，所以不用安装git，下面上查看git 版本，如果您当前没有安装git 请先安装git
```
git version
```

- Terminal 配置个人信息（注意填写的是自己的信息）
```
git config --global user.name "frankie9527"
git config --global user.email "jiangyuhan3730@gmail.com"
```

- Terminal 生成ssh（填写的是自己的邮箱）
```
ssh-keygen -t rsa -C "jiangyuhan3730@gmail.com"
```
输入命令行一直按效果如下为止
![Desktop View](/assets/img/2024-03-30-push-code-github/ssh_finish.jpg){: width="972" height="589" .w-75 .normal}
- Terminal 输入一下查看ssh
```
cat ~/.ssh/id_rsa.pub
```

## 2、添加ssh
- 进入github 界面 --> settings --> SSH and GPG keys
- 点击new ssh
- 拷贝自己ssh到添加界面
  ![Desktop View](/assets/img/2024-03-30-push-code-github/add_ssh_key.jpg){: width="972" height="589" .w-75 .normal}

## 3、github 上创建一个项目并按照 提示就可以上传成功
- git init
- git add README.md
- git commit -m "first commit"
- git branch -M main
- git remote add origin https://github.com/frankie9527/UploadDemo.git
- git push -u origin main

## 4、通过gui上传代码
![Desktop View](/assets/img/2024-03-30-push-code-github/down_load_git_desk.jpg){: width="600" height="489" .w-50 .left}
![Desktop View](/assets/img/2024-03-30-push-code-github/gui_push.jpg){: width="972" height="589"}

 

