# PostgreSQL使用簡介

## 1. 在本地端安裝 postgresql

請至下方兩個連結在電腦上安裝`PostgreSQL Sever`及`pgadmin`。

* [PostgreSQL Server](https://www.postgresql.org/)
* [資料庫管理工具：pgadmin](https://www.pgadmin.org/)

`PostgreSQL`安裝時通常會連帶地安裝命令列工具`psql`，使用者可以直接從命令列打入`psql`開始使用`PostgreSQL`，或使用另外安裝的`pgadmin`來管理`PostgreSQL`。

## 2. 使用 docker 執行 postgresql

### 安裝docker destop

請至下方連結選擇對應的docker desktop安裝。

* [Docker Desktop](https://www.docker.com/products/docker-desktop/)

### 啟動 postgresql server

```bash
docker run --name my_postgres -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -v /path/to/your/local/directory:/var/lib/postgresql/data -d postgres
```

參數說明：

`--name`: 設定 docker container 名稱。

`-e`: 設定環境變數，`POSTGRES_PASSWORD`是資料庫管理者密碼。

`-p`: 設定 port 映射。冒號前面是 host 的 port，後面是 container 的 port。

`-v`: 設定磁碟的映射。冒號前面是host的路徑，後面是container的路徑。目的是為了讓 docker container 裡面的 server 儲存資料時，最後存到 host 的特定目錄去。

`-d`: 設定欲執行的docker image。postgres是postgresql官方提供的docker image。可以使用`-d postgres:版本`來指定版本，譬如：`-d postgres:16.0`或`-d postgres:latest`。

### 使用 docker 執行 `psql` 客戶端

```bash
docker exec -it my_postgres psql -U postgres
```

參數說明：

`-it`: 表示打開`my_postgres`的互動式terminal。

`exec`: 執行`psql`。

`-U`: 表示使用者名稱為`postgres`，這是postgresql server預設的管理者名稱。




