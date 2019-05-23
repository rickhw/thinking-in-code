# 實作分散式 Rate Limit

* 難易度：4/5
* 實作時間：1w

## 題目

使用 node.js (8 以上) 設計一個 library (底下稱為 Omega)，用來限流 (Rate Limit) HTTP Request，這個 Library 必須滿足以下需求：

* 分散式 Rate Limit：多個 container 共用一個限流值，例如限流值是 100 RPS，同時跑 5 個 container，每個則可以處理 20RPS.
* 實作 Client 驗證程式，用來確認 Server Side 是否滿足需求
* 架構示意圖 (TODO)
    * nginx
    * app1 + app2 + app3 + ... + appN
    * redis 

注意：

* backend 架構可以自行選擇適合的 middleware 實作，例如 nginx, redis, ... etc.
* 不可以使用 nginx 的 rate limit (用了還寫啥扣XD)

---

## 交付

1. 一個在 github 的 repos, 包含以下：
    * Omega 的 source code (node.js)
    * Dockerfile: 一個 api server，使用 Omega. 提供 /omega 介面
    * backend docker-compose
1. server side: 透過 docker-compose 起一個 service, 並提供一個 endpoint, 例如 http://127.0.0.0:3000/test
    ** 將 log 寫成 csv，以利透過 spreadsheet 統計每秒的 request count 是否符合需求，格式如下：
```bash
# Date, Time, ContainerName, Path
2019/02/13,12:00:003,Container1,/test
2019/02/13,12:00:034,Container1,/test
2019/02/13,12:00:095,Container1,/test
2019/02/13,12:00:135,Container1,/test
```
1. client side: 指定 RPS 參數，例如指定 100RPS。可以用 docker environment variable.
    *1.* 將 log 寫成 csv，以利透過 spreadsheet 統計.
```bash
## start backend cluster, specify rate limit as 100RPS
docker-compose up -e RL=100

## run client simulator
docker run -ti client -e RPS=10
```

## 驗證

```
# -------#
# Case 1 #
# -------#
## start backend cluster, specify rate limit as 100RPS
docker-compose up -e RL=100

## run client simulator, 
docker run -ti client -e RPS=10
## return sent 10 HTTP Request, reject 0 Reuqest.

# -------#
# Case 2 #
# -------#
## start backend cluster, specify rate limit as 100RPS
docker-compose up -e RL=100

## run client simulator
docker run -ti client -e RPS=150
## return sent 100 HTTP Request, reject 50 Reuqest.

# -------#
# Case N #
# -------#
# 請自行增加 test case.

```

