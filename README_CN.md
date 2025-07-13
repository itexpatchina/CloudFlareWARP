# 中国大陆使用 WARP VPN 指南

本文档介绍了如何在中国大陆使用 Cloudflare 提供的免费 VPN 服务 —— WARP 和 1.1.1.1。

<img src="https://one.one.one.one/media/warp-plus.png"/>

## WARP 应用在中国的当前状态

截至 2025 年，Cloudflare 的 WARP 和 1.1.1.1 应用在中国大陆的网络环境下 **基本无法稳定使用**。相比之下，2023 年的大部分时间内，这些应用在 iPhone、Android 和 PC 上表现良好。

目前，虽然仍可通过非中国区 Apple ID 或 Google Play 账户下载和安装该应用，但要成功连接 WARP 服务几乎变得不可能。

许多国内科技 YouTuber 推测 Cloudflare 的入口 IP 已被中国防火长城（GFW）封锁，这一说法相当可信。Cloudflare 官方公开的 WARP 入口 IP 可查看：  
🔗 [Cloudflare WARP Ingress IPs](https://developers.cloudflare.com/cloudflare-one/connections/connect-devices/warp/deployment/firewall/#warp-ingress-ip)

### WireGuard 协议 IP 范围（2025-07-13 引自 Cloudflare）

- **IPv4 范围**：`162.159.193.0/24`  
- **IPv6 范围**：`2606:4700:100::/48`  
- **默认端口**：`UDP 2408`  
- **备用端口**：  
  - `UDP 500`  
  - `UDP 1701`  
  - `UDP 4500`

## 通过 Telegram 机器人生成 WireGuard 配置

由于 WARP 实质上是基于 WireGuard 协议的服务，因此可通过配置文件提取或生成兼容 Cloudflare 的连接。

以下是我常用的 Telegram 机器人工具：

<img width="335" height="442" alt="Telegram Bot Interface" src="https://github.com/user-attachments/assets/789096c1-7ee5-48c2-8995-a9962e4c7e71" />

只需向该机器人发送 `/generate` 指令，即可获取一个名为 `wg-config.conf` 的 WireGuard 配置文件，可直接导入 WireGuard 官方客户端（适用于 iOS、Android、Windows 等）。

<img width="450" height="188" alt="Generated WireGuard Config File" src="https://github.com/user-attachments/assets/9be0fe66-215d-4da5-b661-e60c1c4f84ad" />

## WireGuard 配置在中国大陆的限制

以下是通过 Telegram 机器人生成的示例配置文件（关键内容已截断）：

<img width="412" height="175" alt="Sample WireGuard Configuration" src="https://github.com/user-attachments/assets/85de15ed-373f-4fa6-a220-8a40833430e5" />

尽管配置看似无误，但在中国大陆环境下 **大概率无法正常连接**，原因主要与 DNS 解析机制和 GFW 干预有关：

- 默认的连接地址 `engage.cloudflareclient.com:2408` 会解析为靠近用户地理位置的 Cloudflare IP。
- 这些本地 IP 往往已被防火长城封锁，导致连接失败。
- 使用官方 WARP 应用也存在相同的问题，点击“连接”按钮时实际上也是尝试连接这些不可达的 IP。

因此，即使配置文件有效，也通常需要额外手动干预，才能在中国大陆实现稳定连接。

## 寻找可用的连接端点

虽然 `engage.cloudflareclient.com:2408` 经常失效，但 Cloudflare 部分入口 IP 仍可能可达。

YouTuber **yonggekkk** 在 GitHub 上发布了一套用于扫描可用 IP 和端口的脚本工具：  
🔗 GitHub 项目地址：[warp-yg](https://github.com/yonggekkk/warp-yg)  
📦 Windows 专用脚本包：[下载 ZIP](https://github.com/yonggekkk/warp-yg/raw/refs/heads/main/WIN%E7%AB%AFwarp%E8%87%AA%E9%80%89IP-v23.11.15.zip)

> ⚠️ **安全提醒**：  
> Windows Defender 可能会将该脚本部分内容识别为风险项。建议在与主机同网段的 **虚拟机中运行** 以确保安全。

> 🈶 **语言说明**：  
> 脚本的菜单界面为中文，具备基础中文阅读能力将有助于操作。

<img width="260" height="55" alt="Script Running Screenshot" src="https://github.com/user-attachments/assets/9ef05c97-6b29-4f6b-a2a5-705a2fc3fd2b" />

## 在 WireGuard 中使用可用端点

运行脚本后会生成一个 `result.csv` 文件，包含可用的 IPv4 地址和端口组合。你可以将其中一个有效 IP 替换原配置文件中的默认端点。

## 📥 下载历史测试结果文件

以下为我在之前测试过程中上传的两个 CSV 文件，存放于本项目的主目录下，可用于参考或进一步分析：

- [`result1.csv`](https://github.com/itexpatchina/CloudFlareWARP/raw/main/result1.csv)
- [`result2.csv`](https://github.com/itexpatchina/CloudFlareWARP/raw/main/result2.csv)

例如，如果确认 `162.159.192.86:1387` 可用，只需将配置文件中的行修改为：  
`Endpoint = 162.159.192.86:1387`

<img width="272" height="79" alt="image" src="https://github.com/user-attachments/assets/13171155-679a-4762-8260-5d0676b5d5cc" />

## Windows 11 上的 WireGuard 演示

以下是在 Windows 11 系统中运行 WireGuard 的演示截图：

<img width="549" height="507" alt="image" src="https://github.com/user-attachments/assets/f73528b2-7859-499d-9041-799fda4fac5a" />

点击 **Activate** 激活按钮后，通常可以成功连接。WireGuard 面板会显示实时传输数据，例如：

> `已接收 XX KiB，已发送 YY KiB`

<img width="553" height="506" alt="WireGuard Transfer Panel" src="https://github.com/user-attachments/assets/ecd2563d-2277-45e1-bdf6-e74e1eee7b91" />

### 连接验证

- 例如通过 ping Google 来确认外网可达性：

<img width="625" height="305" alt="Google Ping Success" src="https://github.com/user-attachments/assets/e8be78ed-53b1-43c2-9dd6-f1778897d3ed" />

- 根据 [whatismyipaddress.com](https://whatismyipaddress.com) 的结果，IPv4 地址仍指向中国境内，通常属于 Cloudflare 数据中心（如上海）：

<img width="778" height="470" alt="Cloudflare IP Location in China" src="https://github.com/user-attachments/assets/025d4048-40e9-4675-9003-4dee6c23de43" />

### 访问限制

即便 WireGuard 隧道已成功建立：

- 诸如 ChatGPT、Claude 等 AI 服务平台仍然不可访问：

<img width="408" height="374" alt="AI Site Blocked" src="https://github.com/user-attachments/assets/a7c09130-8940-462a-bc7d-9581619e819d" />

- Netflix 等流媒体服务也因地域限制而无法播放：

<img width="528" height="72" alt="Netflix Access Denied" src="https://github.com/user-attachments/assets/58451dd3-8628-49fb-8c8d-810d8c25d013" />

### 可访问服务

好消息是，一些原本在中国被屏蔽的网站，如 Google、Facebook、YouTube、X（原 Twitter）和 Instagram 可以顺利打开，且速度较为理想：

<img width="500" height="286" alt="Google Homepage Access Restored" src="https://github.com/user-attachments/assets/deb53908-8a2a-4cd6-a16c-de01fecd2652" />

## 总结

尽管 Cloudflare WARP 基于强大的 WireGuard 协议，在中国大陆仍受到 GFW 严重干扰。然而，通过社区工具和入口扫描脚本，仍可手动配置可用 IP 和端口，实现一定程度的网络自由。虽然 Netflix 和 AI 等平台访问仍受限，但 Google、YouTube、Facebook 等关键服务的可达性得以恢复。本指南从配置生成到实际测试，提供了详实的操作流程，旨在为寻求突破封锁的用户提供实用参考。

## ⭐ 支持本项目

如果你觉得本指南有帮助，不妨在 GitHub 上点个 ⭐Star！这不仅是对作者的鼓励，也有助于更多人发现该项目。Star 还方便你跟进后续更新与新技巧。

让我们一起，从每一个配置文件开始，构建更开放、更透明的技术社区。

