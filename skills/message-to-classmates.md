🚨 不知道你们有没有遇到这个情况——

**你的 Agent 跟你说「讲座 12:00 开始」，结果晚上 8 点才开讲？？**

如果你也在用 Hermes 或者其他 Agent 查 WCB 课程表，大概率遇到过——Agent 报的时间跟你本地时间差了好几个小时。别慌，不是 Agent 傻了，是 WCB API 返回的都是 UTC 时间，Agent 没给你转成你所在时区。

**修一下就好了，以后不再错 👇**

---

**第一步：终端运行安装命令**

```bash
hermes skills install https://raw.githubusercontent.com/emptyshell424/ai-web3-school-cohort-0/main/skills/SKILL.md
```

**第二步：告诉你的 Agent 一句话**

> 以后处理 WCB 时间数据时，自动加载 wcb-timezone skill。

---

搞定 ✅ 之后你的 Agent 会自动读你 WCB 账号里的时区设置，不管是北京、纽约还是东京，时间都给你转成对的。
