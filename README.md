# ⚡ Eternodes 自动续期

自动每28天在 Eternodes Discord 服务器发送 `/server renew` 并选择服务器，在续期窗口期内自动完成续期。

## 使用方法

### 1. Fork 本仓库

点击右上角 **Fork** 按钮。

### 2. 设置 GitHub Secrets

进入你 Fork 后的仓库 → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

| Secret 名称 | 是否必填 | 说明 | 格式 |
|-------------|----------|------|------|
| `DISCORD_TOKEN` | ✅ 必填 | Discord 账号 Token | 打开 Discord 网页版 → F12 → Network → 任意请求 → Headers → `authorization` |
| `SESSION_ID` | ✅ 必填 | Discord Session ID | F12 → Network → 找一个 `interactions` 请求 → Payload → `session_id` |
| `GOST_PROXY` | ⭕ 可选 | 代理地址，不填则直连 | `socks5://user:pass@host:port` |
| `TG_BOT` | ⭕ 可选 | Telegram 通知，不填则跳过 | `CHAT_ID,BOT_TOKEN` |

### 3. 修改脚本中的个人信息

编辑 `eternodes_renew.sh`，将以下变量替换为你自己的信息：
```bash
USER_ID="你的Discord用户ID"    # F12 → 任意请求 → Headers → 找 X-Discord-User-ID，或右键个人头像→复制用户ID
SERVER_VALUE="你的服务器ID"     # 在 Eternodes Bot 回复的下拉菜单中，F12 抓包 → interactions → Payload → values
```

### 4. 启用 Actions

进入你的仓库 → **Actions** → 点击 **Enable** 启用工作流。

### 5. 运行

- **自动运行**：每天 UTC 03:00 自动执行，续期窗口期内会成功，窗口期外会失败但不影响
- **手动运行**：Actions → Eternodes 续期 → Run workflow

## 续期窗口说明

Eternodes 的续期有时间窗口限制，例如 `Window: from 04/03/2026 until 04/17/2026`，只有在窗口期内才能成功续期。脚本每天都会尝试，窗口期外失败属于正常现象，无需担心。

## ⚠️ 注意事项

- 本脚本仅供学习研究，使用前请了解 [Discord 服务条款](https://discord.com/terms)
- **请勿**将你的 `DISCORD_TOKEN` 泄露给任何人
- Secrets 在 GitHub 中是加密存储的，Fork 后他人无法看到你的配置
