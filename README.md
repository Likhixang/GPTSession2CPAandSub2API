<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://img.shields.io/badge/Session_Converter-2c2c2e?style=for-the-badge&logo=json&logoColor=white">
    <img src="https://img.shields.io/badge/Session_Converter-f5f5f7?style=for-the-badge&logo=json&logoColor=333" alt="Session Converter">
  </picture>
</p>

<p align="center">
  <strong>ChatGPT Web Session → CPA · Sub2api · Cockpit · 9router · Codex · Axonhub · Codex-Manager</strong>
  <br/>
  纯前端格式转换工具，不上传 Token，不写入存储。
</p>

<p align="center">
  <a href="https://converter.khixang.cc.cd/"><b>🚀 立即使用</b></a>
  ·
  <a href="#支持输入">支持格式</a>
  ·
  <a href="#输出格式">输出对照</a>
  ·
  <a href="#本地使用">本地部署</a>
</p>

---

## 功能

- **7 种输出格式** — CPA / Sub2api / Cockpit / 9router / Codex / Axonhub / Codex-Manager 一键切换
- **智能探测** — 递归解析 JSON，自动发现 session 对象，兼容 5 种输入源
- **JWT 增强** — 从 accessToken 的 JWT payload 中提取邮箱、账号 ID、计划类型、过期时间
- **合成 ID Token** — 缺失真实 id_token 时自动构造 Codex 可解析的占位 JWT
- **高对比度** — 强调色自动计算文字对比度，浅色底用深字，深色底用白字
- **主题切换** — 亮色 / 暗色 / 跟随系统，设置持久化
- **批量处理** — 多文件拖入，自动分组导出 ZIP
- **无后端** — 所有逻辑在浏览器本地完成，不上传任何数据

## 在线使用

```
https://converter.khixang.cc.cd/
```

[**》》 点我直接使用 《《**](https://converter.khixang.cc.cd/)

## 支持输入

| 来源 | 关键字段 |
|---|---|
| ChatGPT Web Session | `user.email`, `accessToken`, `sessionToken`, `expires`, `account.id`, `account.planType` |
| 9router Codex OAuth | `accessToken`, `refreshToken`, `expiresAt`, `providerSpecificData` |
| Codex auth.json | `auth_mode`, `tokens.access_token/refresh_token/id_token/account_id` |
| Axonhub auth.json | `tokens.access_token/refresh_token/id_token` |
| Codex-Manager | `tokens.access_token/refresh_token/id_token`, `meta.label` |

页面自动从 accessToken 的 JWT payload 中补充邮箱、账号 ID、用户 ID、计划类型和过期时间。

## 输出格式

| 格式 | 用途 | 刷新令牌缺省处理 |
|---|---|---|
| **CPA** | Codex CPA auth JSON | 保留空字符串 |
| **Sub2api** | CPA2sub2API 兼容格式 | expires_at 取自 JWT，auto_pause_on_expired 自动暂停 |
| **Cockpit** | Cockpit Tools Codex 导入 | 保留空字符串 |
| **9router** | 9router Codex OAuth JSON | 保留原始字段 |
| **Codex** | 原生 Codex auth.json | 保留空字符串 |
| **Axonhub** | Axonhub Codex auth.json | 写入 `__missing_refresh_token__` 占位符 |
| **Codex-Manager** | 批量导入 JSON | 保留空字符串，避免误判为可刷新 |

> ChatGPT Web session 通常不包含 OAuth 文件里常见的 `refresh_token`，转换后 access token 过期不能自动刷新。

## 本地使用

```bash
# 直接浏览器打开
open docs/index.html
# 或用任何 HTTP 服务托管
python3 -m http.server 8899 -d docs/
```

无需装依赖，一个 HTML 文件全搞定。
