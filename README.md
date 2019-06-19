# Docker 基礎技術

主要記載一些常見指令及特殊用途指令等，以及一些小範例，方便日後回頭複習使用。

## Basic 概念

***Image***

映像檔，傳統映像檔很大，使用docker 描述的映像檔體積輕巧許多，更方便使用及傳輸。

***Container***

容器，利用映像檔所創造，一個 Image 可以同時創造許多個Container。

Container 可以被啟動、開始、停止、刪除，環境互相分離。（可使用指令使其網路聯通。

## Basic 指令

***查看所有 images***

```cmd
docker images
```

***刪除指定 image***

```cmd
docker rmi IMAGE
```

***查看運行中的 containers***

```cmd
docker ps
```

***查看所有 containers(包含已關閉)***

```cmd
docker ps -a
```

***新建 container***

```cmd
docker run [OPTIONS] IMAGE [COMMAND]
```

常見 OPTIONS 指令包含以下幾個

`-it` 代表在顯性層執行

`-d` 代表在背景層執行，執行完不會留在terminal中

`-p` 映射port，使用方式為 -p 8081:80，冒號左側為local端port，右側為container端port

`-v` 掛載volume，預設關閉container，內容會消失，若需要保留資料等，可掛載本地端位置給container使用，

     使用方式為 -v ./web/:/var/www/html/，冒號左側為本地端volume，右側為container端port

`--rm` 設置此設定後，當關閉該container時，會自動刪除關閉的container

`--name` 設置開啟container的name

`--net` 設置開啟container使用的網路模式

***啟動 container***

```cmd
docker start CONTAINER
```

***停止 container***

```cmd
docker stop CONTAINER
```

***重新啟動 container***

```cmd
docker restart CONTAINER
```

***刪除 container***

```cmd
docker rm CONTAINER
```

***進入 Container***

進入正在執行的container的terminal中

```cmd
docker attach CONTAINER
```

以指定方式進入container中並開啟新terminal

```cmd
docker exec -it CONTAINER bash
```

***查看 Container詳細資料***

```cmd
docker inspect CONTAINER
```

***查看 Container的 Log***

```cmd
docker logs CONTAINER
```

`-f` follow log output

```cmd
docker logs -f CONTAINER
```

***查看 Container的 使用資源***

```cmd
docker stats CONTAINER
```

***暫時停止 Container內 所有行程***

```cmd
docker pause CONTAINER
```

與 stop 不同，stop 是直接終止整個容器，pause只將內部行程關閉，container還是在運作

使用 unpause 可恢復行程

```cmd
docker unpause CONTAINER
```

***停止所有正在運行的 Container***

```cmd
docker container stop $(docker ps -q)
```

***刪除所有已關閉的 Container***

```cmd
docker container prune
```


## Volume 其他 (待補充)

***查看 Volume 清單***

```cmd
docker volume ls
```

***新建 Volume***

```cmd
docker volume create [OPTIONS] [NAME]
```

***刪除 Volume***

```cmd
docker volume rm [OPTIONS] VOLUME
```

***查看 Volume 詳細資料***

```cmd
docker volume inspect [OPTIONS] VOLUME
```

***刪除全部未使用的 Volume***

```cmd
docker volume prune
```

## Network 其他（待補充）

關於network ，建議可先了解docker 的基本4種網路模式，bridge, host, container, none。

參照[Docker網路管理（容器的四種網路模式）](https://www.itread01.com/content/1542573736.html)

有助於後續學習與加深理解。

`bridge` 為預設使用

***查看 network 清單***

```cmd
docker network ls
```

***指定 network ***

```cmd
docker run -it --rm --net=bridge ubuntu bash
```

***建立 network***

```cmd
docker network create [OPTIONS] [NAME]
```

***移除 network***

```cmd
docker network rm NETWORK
```

***移除全部未使用的 network***

```cmd
docker network prune
```

***查看 network 詳細資料***

```cmd
docker network inspect [OPTIONS] NETWORK
```

***將 container 連接 network***

```cmd
docker network connect [OPTIONS] NETWORK CONTAINER
```

***斷開 container 所連接 network***

```cmd
docker network disconnect [OPTIONS] NETWORK CONTAINER
```


## 其他使用指令

***Container 中查看 LINUX版本***

```cmd
cat /etc/os-release
```

***Container 中查看 網路設定***

```cmd
cat /etc/hosts
```

***儲存image 為tar 檔案***

```cmd
docker save busybox > busybox.tar
```

***載入image***

```cmd
docker load < busybox.tar
```