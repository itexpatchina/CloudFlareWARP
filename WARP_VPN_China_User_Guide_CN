# 🎬 WARP VPN 中国大陆使用教程：YouTube 视频脚本（中文）

## 开场白（0:00–0:30）

大家好，欢迎来到 **IT Expat** 频道。我是一名专注于技术教程的内容创作者。

你是否曾经尝试过使用 WARP VPN，却始终无法在中国大陆连接成功？  
在本视频中，我将一步步教你如何生成 WireGuard 配置、绕过 GFW 干扰，并连接 Cloudflare WARP。

---

## 第 1 部分：WARP 在中国大陆为什么无法使用（0:30–1:30）

从 2024 年底起，Cloudflare 的官方 WARP 和 1.1.1.1 应用在中国大陆已经难以正常连接。  
主要原因是它们的入口 IP 被 GFW（防火长城）屏蔽了。

Cloudflare 公布的 WireGuard 接入网段如下：

- IPv4：`162.159.193.0/24`
- 默认端口：`UDP 2408`，备用端口为 `500 / 1701 / 4500`

你可能仍然能下载 App，但点击“连接”按钮时永远停留在“正在连接”阶段。

---

## 第 2 部分：用 Telegram Bot 生成 WireGuard 配置（1:30–3:00）

我们可以使用 Telegram 上的一个机器人，通过 `/generate` 命令快速生成配置文件。

生成后，你将获得一个名为 `wg-config.conf` 的文件，可以直接导入 WireGuard 应用（支持 iOS / Android / Windows）。

> 小贴士：Telegram 在中国大陆也可能需要科学上网访问。

---

## 第 3 部分：配置文件在中国仍无法连接的原因（3:00–4:00）

配置看起来是有效的，但由于默认的连接端点是：

```
engage.cloudflareclient.com:2408
```

DNS 会解析出一个离你地理位置最近的 Cloudflare 入口 IP，**而这些 IP 通常都被屏蔽**。

这就是为什么即使导入成功，你也无法连接。

---

## 第 4 部分：使用 yonggekkk 脚本扫描可用 IP（4:00–6:00）

B站和 GitHub 上的 up 主 yonggekkk 提供了一个 Windows 脚本，可以批量测试可用 IP+端口组合。

你可以在他的 GitHub 仓库下载：

- 仓库地址：[warp-yg](https://github.com/yonggekkk/warp-yg)
- 脚本包下载：[点击下载](https://github.com/yonggekkk/warp-yg/raw/refs/heads/main/WIN%E7%AB%AFwarp%E8%87%AA%E9%80%89IP-v23.11.15.zip)

⚠️ 建议在虚拟机中运行脚本，避免主机报毒或存在潜在风险。  
🈶 脚本是中文界面，操作简单，支持交互菜单。

脚本运行完毕后会输出一个 `result.csv`，其中列出了可用的 IP 列表。

---

## 第 5 部分：修改配置文件并连接（6:00–7:30）

用你从 `result.csv` 中找到的 IP 替换配置文件中的默认地址，例如：

```
162.159.192.86:1387
```

保存后，打开 WireGuard 客户端，点击“激活”按钮。

如果设置正确，你会看到数据开始传输：

```
接收 XX KiB，发送 YY KiB
```

---

## 第 6 部分：实际测试效果与限制（7:30–9:00）

### ✅ 可以访问：
- Google / YouTube / Facebook / Instagram / Twitter（现称 X）
- 大多数常见被墙网站，速度尚可

### ❌ 无法访问：
- Netflix（地区限制）
- AI 平台：如 ChatGPT、Claude、Gemini 等

根据 [whatismyipaddress.com](https://whatismyipaddress.com) 显示，你的 IP 可能仍显示为中国地区的 Cloudflare 节点（如上海）。

---

## 结尾 + 呼吁行动（9:00–10:00）

虽然 Cloudflare WARP 在中国大陆连接受限，但通过 Telegram 工具和 IP 扫描脚本，我们仍然可以配置出一个基本可用的 VPN。

如果你觉得本视频有帮助，请：

- 点赞 👍
- 订阅 📥
- 留言 💬
- 在 GitHub 给本项目点 ⭐️

我是 **IT Expat**，我们下期再见！

---

## 💡 附加建议

你也可以参考项目中的中文文档：

👉 [📘 中文版说明文档](./readme_cn.md)

GitHub 项目地址：`https://github.com/你的用户名/你的项目名`
