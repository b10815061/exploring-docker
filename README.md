# exploring-docker

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
