# 时序 · 云同步日程管家

全中文网页。用户名+密码注册，无手机号、微信或邮箱；账号独立、跨设备同步。日历按小时/日/周/月/年查看，支持事项、目标、备忘、完成打勾、收支账本和时间统计。

## 部署（推荐 Render + Neon 免费计划）

1. 到 https://console.neon.tech/ 注册/登录，创建一个免费的 PostgreSQL 项目，点击 **Connect**，复制完整连接字符串（`postgresql://...`）。这是数据库密码，**不要提交到 GitHub 或公开截图**。
2. 把本项目文件上传到一个新 GitHub 仓库（`package.json`, `server.js`, `public/` 和此说明必须放在仓库根目录）。
3. 在 Render 新建 **Web Service**，选择仓库，Language 选 Node，Build Command 填 `npm install`，Start Command 填 `npm start`，实例类型选 **Free**（若可用）。
4. 在 Render 的 **Environment Variables** 添加：`DATABASE_URL` = Neon 连接字符串；`NODE_ENV` = `production`。请使用环境变量，绝不把数据库连接字符串写到源码里。
5. 部署，日志出现「时序日历已启动」后，访问 Render 提供的 HTTPS 网址。首次部署会自动建立数据表。
6. 在浏览器注册一个账号，再用另一个设备访问**同一个网址**并登录同一账号，查看同步。

## 安全和使用提醒

- 密码只存储 bcrypt 哈希；登录态采用 Secure/HttpOnly cookie（HTTPS 部署）；每个请求按登录账号隔离数据。登录有效期 30 天。
- 没有绑定邮箱或手机号，也没有密码找回。忘记账号密码可能永久失去访问权；请使用密码管理器，定期在「我的账号」导出 JSON 备份。
- Render 免费 Web Service 会休眠；本项目**不能**用 Render 本地 SQLite/JSON 当数据库。Neon 作为独立数据库，Render 服务重启后数据仍在。
- Render、Neon 的免费方案有资源、访问限制，未来政策可能调整。正式存储敏感财务数据前，请自行评估安全和备份需求。本项目是个人使用基础版，没有微信通知和微信登录。
- 若多人共用账号会看到同一份数据；不同账号互相隔离。对常用手机建议添加网页到主屏幕。
