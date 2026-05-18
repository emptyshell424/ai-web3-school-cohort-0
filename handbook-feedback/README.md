# Handbook Feedback 流程

> 你的问题、卡点、错别字、概念不清、资料过期、结构建议，都可以整理到这里。

## 反馈格式

每条 feedback 一个文件，命名：`YYYY-MM-DD-简短描述.md`

### 模板

```markdown
# Feedback: [简短标题]

## 来源
- **Handbook 页面**: [链接]
- **日期**: YYYY-MM-DD
- **类型**: 错别字 / 概念不清 / 资料过期 / 结构建议 / 其他

## 问题描述
[具体描述哪里有问题]

## 建议改法
[你觉得应该怎么改]

## 参考来源（可选）
[如有参考链接或资料]
```

## 示例

```markdown
# Feedback: Wallet 章节缺少 AA 对比

## 来源
- **Handbook 页面**: https://aiweb3.school/zh/handbook/web3/wallet/
- **日期**: 2026-05-18
- **类型**: 概念不清

## 问题描述
Wallet 章节提到了 EOA 钱包但没有跟 Smart Account（AA）做对比，新手容易混淆两者的区别。

## 建议改法
加一段对比表格：EOA vs Smart Account 在权限、签名方式、Gas 支付等方面的区别。
```

## 提交流程

1. 写 feedback → 放到 `handbook-feedback/` 目录
2. commit + push 到 GitHub
3. 如需提交到官方仓库，我们再搬运到 [lxdao-official/aiweb3school](https://github.com/lxdao-official/aiweb3school)
