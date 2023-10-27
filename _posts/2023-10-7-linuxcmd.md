---
layout:       post
title:        "Linux系统查看端口的命令"
author:       "zxg"
header-style: text
catalog:      true
tags:
    - Linux
---

### Linux系统查看端口的命令

- netstat -tuln
  
  > ```cpp
  > -t: tcp
  > -u: udp
  > -l: 展示正在监听的socket
  > -n: 以数字形式显示端口号，而不是名称
  > ```

- lsof -i
  
  > list open files，显示系统中所有打开的文件和进程，可以指定端口号
  > 
  > eg: lsof -i :80

- ss -tuln
  
  > 显示所有套接字
