# ⚠️ 注意

**本项目旨在优化 CDN 网络访问速度，请勿用于非法用途！**

本项目最早是 Fork [`Hackl0us/GeoIP2-CN`](https://github.com/Hackl0us/GeoIP2-CN) 定制修改而来。

# GeoIP2 · CN

**本项目使用 GitHub Actions 每周五自动更新。**

## 📥 下载链接
| 📦 项目 | 📃 文件 | :octocat: GitHub RAW |  🚀 CDN 加速 | 🔧 适用范围
|  :--:  |  :--:  |     :--:     |     :--:    | ---- |
| IP-CIDR 列表 | CN-ip-cidr.txt | [点我下载](https://raw.githubusercontent.com/mangoclover/GeoIP2-CN/release/CN-ip-cidr.txt) |  [点我起飞](https://cdn.jsdelivr.net/gh/mangoclover/GeoIP2-CN@release/CN-ip-cidr.txt) | iptables, ipset, squid, gost, 3proxy, etc.  | 
| GeoIP2 数据库 | Country.mmdb | [点我下载](https://github.com/mangoclover/GeoIP2-CN/raw/release/Country.mmdb) |  [点我起飞](https://cdn.jsdelivr.net/gh/mangoclover/GeoIP2-CN@release/Country.mmdb) | Surge, Shadowrocket,<br>QuantumultX, Clash<br>等较新的代理工具|
| Surge规则集 | Surge-Ruleset.list | [点我下载](https://raw.githubusercontent.com/mangoclover/GeoIP2-CN/release/Surge-Ruleset.list) | [点我起飞](https://cdn.jsdelivr.net/gh/mangoclover/GeoIP2-CN@release/Surge-Ruleset.list) | Surge |

> 如果无法访问**GitHub Raw**域名 `raw.githubusercontent.com`，可以使用**CDN加速地址**（`cdn.jsdelivr.net`），**而且内容更新0延迟**。

## 🙋🏻‍♂️ 使用方式（以GeoIP2 数据库为例)

⚠️ 注意：任何代理工具在使用本项目提供的数据库前，请务必确保以下 3 点（请根据工具语法调整规则）：
* 禁用与 中国大陆 IP 地址段 直连策略 相关的规则或规则集
    ``` bash
    RULE-SET, https://raw.githubusercontent.com/mangoclover/ios_rule_script/master/rule/Surge/ChinaIPs/ChinaIPs.list, DIRECT # 务必禁用或删除
    GEOIP, CN, DIRECT # 与上一条类似的规则与本条规则不可共存
    ```

* 规则中使用 `GEOIP, CN, DIRECT` 来调用数据库查询，且该条规则建议紧随最终规则之上，避免多余的 DNS 查询，降低效率。
    ``` bash
    ... 省略诸多规则 ...
    GEOIP, CN, DIRECT # 建议在这里使用规则
    FINAL, PROXY # 最终规则
    ```

* 规则中不可以存在其他国家或地区的 `GEOIP` 规则，因为数据库中仅包含中国大陆地区的 IP 地址段记录
    ``` bash
    GEOIP, US, PROXY # 错误，无法查询到相关记录
    GEOIP, AU, PROXY # 错误，无法查询到相关记录
    GEOIP, HK, PROXY # 错误，无法查询到相关记录
    GEOIP, CN, DIRECT # 正确
    ```

### Surge 

**Surge for macOS**

⚠️ 软件版本要求 `4.0.2 (1215) [Beta]` 或更高

打开软件 Dashboard > Setting > General > 在 GeoIP Database 处粘贴上方复制的 `Country.mmdb` 下载链接，点击 Update Now 即可。

**Surge for iOS / iPadOS** 

⚠️ 软件版本要求 `4.10.0 (1851) [TestFlight]` 或更高

打开 App > Home 页面拉至最下 > More Settings > GeoIP Database > 在 CUSTOM GEOIP DATABASE URL 处粘贴上方复制的 `Country.mmdb` 下载链接，点击 Update Now 即可。

**特别的，版本`4.10.0 (1853) [TestFlight]`开始支持自动GeoIP数据库更新，更新频率为每周一次。**

#### ShadowRocket 和 Quantumult X
直接在 Safari 中打开 `Country.mmdb` 下载链接，Safari 下载完毕后页面下方会提示 “在...中打开”，点击完成导入。


# 🏅 版权声明

本项目中[`CN-ip-cidr.txt`](https://raw.githubusercontent.com/mangoclover/GeoIP2-CN/release/CN-ip-cidr.txt)和[`Country.mmdb`](https://github.com/mangoclover/GeoIP2-CN/raw/release/Country.mmdb)所使用的 IP 地址信息来自于 [`17mon/china_ip_list`](https://github.com/17mon/china_ip_list)（基于 ipip.net）和 [`metowolf/iplist`](https://github.com/metowolf/iplist) （基于 纯真 IP）；[`Surge-Ruleset.list`](https://raw.githubusercontent.com/mangoclover/GeoIP2-CN/release/Surge-Ruleset.list)中所使用的 IP 地址信息来自于[`misakaio/chnroutes2`](https://github.com/misakaio/chnroutes2/blob/master/chnroutes.txt)。

GeoIP® 商标版权归 [`MaxMind`](https://www.maxmind.com/) 公司所有。
