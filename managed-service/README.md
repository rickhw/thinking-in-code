
設計、並實作一個 Managed Service，提供可以擴展的 Load Balancer 服務，簡單說就是類似於 AWS 的 ALB，必須滿足以下：

1. 使用者可以自行建置 (provision) 此服務，可以自行選擇部署到三大雲平台，同時產生管理後台。
    1. 選擇 Cloud Provider -> Region
    1. 指定 DNS Mapping
    1. 設定第一個 Rule：upstream、health check
    1. 設定管理帳號與密碼。
    1. 產生管理後台的 URL
1. 管理後台
    * 可以自行管理 upstream 與 `path-based routing` 等 rule-base 配置
    * 支援 Multiple DNS
    * 支援 import / export config, ssl key
    * 支援成本管理
    * 提供 Log 機制
1. 功能
    * 支援 SSL
    * 支援自動擴展 (auto scale)
    * 支援 HTTP 常見的監控指標，像是 Request、Latency、HTTP Code
1. 注意：
    * 必須是最低成本
    * 提供 free triad 功能


[1] https://www.facebook.com/rick.kyhwang/posts/10209644996201104
source: https://www.facebook.com/rick.kyhwang/posts/10212002664781345


2019/10/09


---

[重新貼] 調查看看，大家覺的這個題目難易度：

建立一個系統 (PaaS)，使用者輸入：
- site-id (unique): [A-Za-z0-9]
- email
- 選擇 Wordpress 官方 *任意* GA 版本
- 可以選擇儲存空間大小, 資料庫大小
- 可用 k8s, AWS, 各種現代技術。

Output:
- 自動蓋好整個 Wordpress （含 DB, DNS, WEB), 獨立資源
- 網站 endpoint = {site-id}.abc.com
- 代出 Wordpress 設定算完成 (不含 MySQL 設定)

Verification:
- 輸入 `https://{site-id}.abc.com` 連到使用者的 Wordpress
- 每個使用者的資源是獨立的, 包含 DB, Web, Storage.
* "獨立" 至少是 container level

備註：要寫 code 完成，不限語言。

source: https://www.facebook.com/rick.kyhwang/posts/10209644996201104
date: 2018/07/24