# exploring-docker

docker depends on windows hypervisor & WSL(linux on windows), when hyperV running, we cant start vm but to shut it down;

while we want to do the opposite, we run up hypervisor (locate it at windows key>controll console>uninstall programs>able or disable windows program> find hyperV)

& run CMD with adminstrator > $bcdedit /set hypervisorlaunchtype auto

# docker GUI
開啟xserver；在dockerfile裡面寫```RUN apt update && apt install -y pcmanfm xterm \ ENV DISPLAY=host.docker.internal:0.0 \ CMD pcmanfm```


docker run [flags] [image] [instrcution]

flags : 
        
        1.-it : 配合 /bin/bash可以在terminal打開這個container的bash(使用exec時)

        2.-d(t)  : 背景執行 (每個container跑完[instrcution]就會睡覺，要馬instuction要可以讓他keep waking，不然就使用 -dt)
        
docker exec [flags] [container-id] [instruction]

flags :

        1.-it : 配合 /bin/bash可以在terminal打開這個container的bash(使用exec時)
        
docker ps [flags]

flags:

        1. -a : 秀出所有，沒有加上a的話只會秀出running的
        
        2. -q : 只顯示id，常配合rm使用
        
docker rm [flags] [container-id]

flags:
        
        1. -f : 通常要先stop才可以rm，用-f可以stop+rm
        
        2. container-id的部分可以用類js的寫法，例: docker rm $(docker ps -a -q)，刪除所有container
        
docker volume create --name [name]

建立一個volume讓開啟container時可以使用

```
docker run --name db -e POSTGRES_USER=tommy -e POSTGRES_PASSWORD=0000 -e POSTGRES_DB=campus -v pg-data:/var/lib/postgresql/data -p 5432:5432 -d postgres:12-alpine
```

使用postgres image建立一個container名字叫做db，使用者是tommy且密碼是0000，volume使用pg-data

如果exec以後他說沒有這個user，有可能是volume用到舊的

postgres版本很重要，要使用12-alpine

如果一直顯示密碼錯誤但檢查所有設置都是正確的情況下，有可能是本機的postsql擋住了docker裡面的，這時候去到服務把本機的postsql停止。

# using dockerfile

## first need to build a image


docker build [flag] [path]


flags:

        1.-t : tag : 給這個image一個名字

path:

        Dockerfile所在的位置，.的話就表示現在跟Dockerfile在同一層
        
## then run from the image


docker run [flag] [image-name]


