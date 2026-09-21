# CLAUDE.md

> 本仓库维护一份 Shadowrocket 配置文件 `ddh.conf`。本文件为 Claude Code 提供项目上下文，每次会话优先读取。

## 项目概述

- 仓库路径：`D:\file\project\persion-pj\shadowrocket`
- 核心文件：`ddh.conf`（Shadowrocket 配置）
- 仓库：https://github.com/donghua2023/shadowrocket-conf
- 上游来源：[Johnshall/Shadowrocket-ADBlock-Rules-Forever](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever)
- 自动更新源（`update-url`）：`https://raw.githubusercontent.com/donghua2023/shadowrocket-conf/master/ddh.conf`（自托管，整体自更新）
- 总策略：**国内直连、国外代理**，不含广告过滤
- 文件内标注最后更新：2026-08-14 15:00:45

## ddh.conf 结构索引

| 区块 | 行号 | 说明 |
|------|------|------|
| `[General]` | 2–9 | IPv6 / bypass / DNS / 更新源 |
| `[Rule]` | 11–452 | 分流规则主体（新增直连分组后实际延伸至 523 行） |
| `[URL Rewrite]` | 449 | URL 重写（新增直连条后实际位于 526 行） |
| `[MITM]` | 452 | MITM hostname（新增直连条后实际位于 529 行） |

### [General] 关键项

- `ipv6 = false`（默认关闭）
- `bypass-system = true`
- `skip-proxy`：局域网 + `*.local *.lan *.internal` 等
- `bypass-tun`：大量 IPv4/IPv6 保留段
- `dns-server`：阿里 DoH (`dns.alidns.com`) + 腾讯 DoH (`doh.pub`)
- `update-url`：`https://raw.githubusercontent.com/donghua2023/shadowrocket-conf/master/ddh.conf`（自托管整体配置，非上游 CNIP 片段）

### [Rule] 分组行号

| 分组 | 起始行 | 备注 |
|------|--------|------|
| Google AMP | 18 | |
| TED | 22 | |
| Telegram | 23–43 | 域名 + IP-CIDR（91.108.x / 149.154.160/20 / IPv6） |
| Disqus | 45 | |
| WhatsApp | 47–48 | |
| 台/港/澳 | 50 | `appledaily.tw` |
| Google Voice | 52 | `74.125.0.0/16` |
| Google Ads/Analytics | 54–62 | 作者标注「可能冗余」 |
| 华尔街邮报 | 64 | `dowjones.com` |
| OneDrive/微软 | 66–75 | 作者标注「可能冗余」 |
| Mendeley | 77 | |
| Apple News | 79–91 | |
| GitHub | 93 | `raw.githubusercontent.com` |
| 苹果域名及 CDN | 97–129 | 大量 `*.akadns.net` |
| Disney+ | 131–250 | 全球 `disney.*` + 关联品牌 |
| Amazon / AWS | 252–398 | 含 `DOMAIN-KEYWORD,amazon/aws` |
| Paramount+ | 400 | |
| Bing | 402 | |
| DNS 泄漏测试 | 404–409 | |
| Forefront / Mozilla / Txt.fyi | 411–415 | |
| Adobe / AOL / Yahoo | 417–421 | |
| LinkedIn | 423–424 | |
| Copilot | 426 | |
| hoyolab | 428 | |
| 防止 Bing 地区检测 | 430 | `location.microsoft.com` |
| devv | 432 | |
| 蔚蓝档案日服 | 434 | 绕过中国 IP 检测 |
| Minecraft 下载加速 | 436–437 | |
| GitHub 在线编辑器 | 439 | `github.dev` |
| Minecraft 3D 头颅修复 | 441 | `mc-heads.net` |
| 越狱下载源加速 | 443–444 | |
| Binance 币安直连 | 446–453 | `DOMAIN-SUFFIX` + `DOMAIN-KEYWORD,binance` |
| MT5 / MetaTrader 直连 | 455–459 | `metatrader5.com` 等 + `DOMAIN-KEYWORD,metaquotes` |
| 同花顺直连 | 461–464 | `10jqka.com.cn` / `myhexin.com` + `DOMAIN-KEYWORD,hexin` |
| 微信直连 | 466–470 | `weixin.com` / `wechat.com` + `DOMAIN-KEYWORD,weixin` |
| QQ 直连 | 472–478 | `qq.com` / `gtimg.com` + `DOMAIN-KEYWORD,qq` |
| 抖音直连 | 480–485 | `douyin.com` / `ixigua.com` / `snssdk.com` + `DOMAIN-KEYWORD,douyin` |
| 豆包直连 | 486–489 | `doubao.com` / `doubao.cn` + `DOMAIN-KEYWORD,doubao` |
| 工商银行直连 | 490–494 | `icbc.com.cn` / `icbc.com` / `icbc.com.hk` + `DOMAIN-KEYWORD,icbc` |
| 建设银行直连 | 495–499 | `ccb.com.cn` / `ccb.com` / `ccbqn.cn` + `DOMAIN-KEYWORD,ccb` |
| 上海银行直连 | 500–502 | `bosc.cn` + `DOMAIN-KEYWORD,bosc` |
| 招商银行直连 | 503–507 | `cmbchina.com` / `cmb.com` + `DOMAIN-KEYWORD,cmb` |
| 支付宝直连 | 508–512 | `alipay.com` / `alipay.net` / `alipayobjects.com` + `DOMAIN-KEYWORD,alipay` |
| 云闪付直连 | 513–515 | `95516.com` + `DOMAIN-KEYWORD,95516` |
| 转转直连 | 516–521 | `zhuanzhuan.com` / `zhuaninc.com` / `zhuanzhuan.cn` + `DOMAIN-KEYWORD,zhuanzhuan/zhuaninc` |
| 微信直连(兜底注释) | 522 | 提示已在上方微信分组覆盖 |
| 兜底 | 523–524 | `GEOIP,CN,DIRECT` → `FINAL,PROXY` |

### [URL Rewrite] / [MITM]

- Rewrite（449）：`google.cn` / `g.cn` → `https://www.google.com`（302）
- MITM hostname（452）：`*.google.cn`, `*.googlevideo.com`

## 已知问题 / 待办

1. **拼写错误（疑似）**：第 270 行 `amaaozn.com`，应为 `amazon.com`，目前可能是无效规则。
2. **作者标注「可能冗余」**：第 53 行（Google Ads/Analytics）、第 65 行（OneDrive/微软）。
3. 手写叠加条目（相对上游额外补充）：Minecraft、越狱源、蔚蓝档案、devv / hoyolab / Copilot / Bing 地区等。

## 维护规范

- 新增代理服务：在 `[Rule]` 对应分组下追加 `DOMAIN-SUFFIX,xxx.com,PROXY`，并补一行分组注释。
- 规则自上而下匹配，`GEOIP,CN,DIRECT` 在 `FINAL,PROXY` 之前；`DOMAIN-SUFFIX` 在 `GEOIP` 之前命中即生效。
- 修改 DNS / 更新源后需在 Shadowrocket 内重载配置。
- 开启 IPv6 时同步检查 `bypass-tun` 中 IPv6 段覆盖情况。

## 工作约定

- 编辑 `ddh.conf` 前先读取本文件定位行号，再按需打开对应行段。
- 保留作者原有的中文分组注释风格（`# 分组名`）。
- 不要改动 `[General]` 除非用户明确要求。
- 提交代码到仓库时需要跟我确认，同意之后再提交
