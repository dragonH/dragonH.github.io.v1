---
layout: post
title: 'Ubuntu Server 16.04 安裝 Apache,Mysql,PHP'
date: 2018-04-30 00:00:00 -0800
categories:
    - 'Server'
    - 'Ubuntu'
tags:
    - 'Mysql'
    - 'Apache'
    - 'PHP'
    - 'Ubuntu'
---
記錄一下Ubuntu Server 16.04安裝AMP過程<!-- more -->


<br>
### 1.機器剛啟動先把套件更新一下

    sudo apt-get update


### 2.安裝Apache Server

    sudo apt-get install apache2

#### 設定時間,有設定過的話可以跳過此步驟



    sudo locale-gen zh_TW.UTF-8

#### 將Apache Server重啟

    sudo service apache2 restart


### 3.安裝MYSQL SERVER

    sudo apt-get install mysql-server


### 4.安裝PHP5.6

由於Ubuntu Server 16.04內建的是PHP7.0

為預防一些相容性的問題

可以安裝PHP5.6

之後也可以用指令來切換版本
<br><br>
#### Add the PPA

    sudo add-apt-repository ppa:ondrej/php

#### 安裝PHP5.6

    sudo apt-get update
    sudo apt-get install php5.6

#### 切換PHP版本

(5.6->7.0)

    sudo a2dismod php5.6 ; sudo a2enmod php7.0 ; sudo service apache2 restart

(7.0->5.6)

    sudo a2dismod php7.0 ; sudo a2enmod php5.6 ; sudo service apache2 restart



