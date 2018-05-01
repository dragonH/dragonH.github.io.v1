---
layout: post
title: 'EC2新建使用者並以SSH KEY登入'
date: 2018-05-01 00:00:00 -0800
categories:
    - 'Server'
    - 'Ubuntu'
tags:
    - 'Ubuntu'
    - 'SSH'
---
新建使用者並以SSH KEY登入<!-- more -->

剛安裝完AMP

一定會發現無法對www這個資料夾進行修改或新增檔案

許多網路上的教學都會說直接把資料夾的權限改成777

或者新建一個www-data帳號來登入

但其實是相當不安全的

權限為777表示所有人都可以讀取、寫入、執行

新建www-data來登入的話 

就跟把root設密碼以root登入一樣不安全

因此

最好的辦法就是

新增一個以SSH KEY登入的使用者

在新建一個群組

並讓這個群組擁有www的修改權限

再將新增的使用者加入此群組

<br>
#### 1.新增一個使用者google並設定SSH KEY

    sudo adduser google

切換帳號

    sudo su google

建立 <mark>~/.ssh</mark>這個目錄

    mkdir -p ~/.ssh

設定權限

    chmod 700 ~/.ssh

產生金鑰，基本上都用預設的設定就好

    ssh-keygen -t rsa

修改金鑰檔名

    cd ~/.ssh
    cp id_rsa.pub authorized_keys

複製 id_rsa 的內容並在本機將其存成 google_login.pem

     cat id_rsa

到這裡就算完成,以後登入google這個帳號就是用<mark>google_login.pem</mark>這隻金鑰

<br>
#### 2.新建一個Web群組

    groupadd Web

使Web這個群組擁有www這個資料夾

    sudo chown -R www-data:web /var/www

修改www的權限

775代表的分別是擁有者、擁有群組、所有人

    sudo chmod 775 -R /var/www.

<br>
#### 3.將google這個使用者加入Web這個群組

    useradd -G Web google

以上設定都沒問題的話

以後就可以用google這個使用者來修改www這個資料夾了



