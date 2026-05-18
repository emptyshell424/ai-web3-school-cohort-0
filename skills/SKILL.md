---
name: wcb-timezone
description: "硬性规则：WCB API 返回的时间都是 UTC，必须转换为用户本地时间。用 users.getProfile 获取用户 timezone 字段，做动态转换。"
---

# WCB 时区转换 — 强制规则

**这是硬性规则，不是建议。违反就是 bug。**

## 规则

WCB Agent API 返回的所有 `startAt`、`endAt` 字段都是 **UTC 时间**（末尾带 `Z`）。

用户的本地时区存储在 WCB Profile 中：
```
users.getProfile → timezone 字段（如 "Asia/Shanghai"）
```

**展示给用户前，必须将 UTC 时间转换为用户所在时区的本地时间。**

## 正确做法（通用方案，适用于任何时区）

### 第一步：获取用户时区

```python
import subprocess, json, pytz
from datetime import datetime

# 调 WCB API 获取用户 profile
result = subprocess.run([
    'curl', '-s', '-X', 'POST',
    'https://web3career.build/api/agent/call',
    '-H', 'Authorization: Bearer ' + api_key,
    '-H', 'Content-Type: application/json',
    '-d', '{"procedure":"users.getProfile","input":{}}'
], capture_output=True, text=True)
profile = json.loads(result.stdout)
user_tz_str = profile['result']['timezone']  # e.g. "Asia/Shanghai" / "America/New_York" — 动态读取，不写死

# 转换
utc_time = datetime.fromisoformat(utc_str.replace('Z', '+00:00'))
local_tz = pytz.timezone(user_tz_str)
local_time = utc_time.astimezone(local_tz)
```

### 第二步：转换所有时间

展示给用户前，逐条检查每个时间字段，做 UTC → 本地时间转换。

## 适用范围

- cron 早报
- daily note 中的日程
- 口头回答中的时间
- 任何发给用户的时间信息

## 📤 分享给同学

可直接复制以下内容到群聊/私聊：

---

### 一句话版

> WCB API 返回的时间都是 UTC。告诉你的 Agent：「去 users.getProfile 拿我的 timezone，自动转换到本地时间。」

### Hermes 一键安装版

> **⏰ WCB 时间不对？装个 skill 就搞定**
>
> 终端运行：
> ```bash
> hermes skills install https://raw.githubusercontent.com/emptyshell424/ai-web3-school-cohort-0/main/skills/SKILL.md
> ```
>
> 装完告诉 Agent：「以后处理 WCB 时间时，自动加载 wcb-timezone skill。」
>
> 之后所有时间自动适配你的时区。北京、纽约、伦敦、东京…都能用 🌍

### 非 Hermes 用户版

> 在 Agent 的 prompt 或 system message 里加上：
>
> > WCB 返回的时间是 UTC。先调 `users.getProfile` 获取用户 timezone，把所有 UTC 时间转换到用户本地时区再展示。不写死偏移量，动态读取。

---

## 校验步骤（每次必做）

1. 这个时间从哪来的？WCB API 还是手动写的？
2. 如果是 WCB API → 一定是 UTC，必须通过 `users.getProfile` 拿用户时区来转
3. 如果是手动写的 → 确认用的是本地时间还是 UTC
4. 禁止目测心算，必须用工具/代码转换
5. 如果是给别的同学用 → 让他们先确认自己 WCB Profile 里的 timezone 字段是对的
