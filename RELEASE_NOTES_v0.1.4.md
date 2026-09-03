# Net Tentacle 0.1.4 / 网络触手 0.1.4

## 中文

### 本次更新

- 修复断开或改选 Console 设备时，旧连接任务偶尔把界面错误恢复为“已连接”的问题。
- 提供可与正式版并存的 `Net Tentacle Debug 0.1.4`，仅用于受控测试和问题反馈。
- AI 建议配置在终端页面下方单独核对；黑色终端只保留设备真实 Console 回显。
- 操作日志记录实际提交到设备的人工命令、AI 配置和危险命令触发记录，并隐藏密码、密钥、Token 等敏感行。
- 对明确灾难性命令进行拦截；对高影响命令要求操作员确认已完成备份。

### 安装包

- `Net Tentacle.apk`：正式测试版，适合普通使用者安装。
- `Net Tentacle Debug 0.1.4.apk`：仅供受控测试。它会在本机保留脱敏运行日志；只有测试者主动提交 Bug 后，系统才会打开邮件客户端。

## English

### Highlights

- Fixed a Console connection race where an outdated connection task could incorrectly restore the UI to “connected.”
- Added `Net Tentacle Debug 0.1.4`, which can be installed alongside the production build for controlled testing and feedback.
- AI-suggested configurations are reviewed in a separate panel on the terminal page; the black terminal remains limited to real device Console output.
- The local audit trail records submitted manual commands, AI configurations and dangerous-command triggers while hiding sensitive password, key and token lines.
- Explicitly destructive commands are blocked; high-impact commands require the operator to confirm that a backup has been completed.

### Packages

- `Net Tentacle.apk`: production test build for normal users.
- `Net Tentacle Debug 0.1.4.apk`: for controlled testing only. It keeps sanitized diagnostics locally and opens an email client only after a tester explicitly submits a Bug report.
