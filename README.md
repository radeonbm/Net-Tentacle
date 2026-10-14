<p align="center">
  <img src="net-tentacle-logo.png" width="180" alt="Net Tentacle logo">
</p>

# Net Tentacle / 网络触手

> 一个 Android 手机、一根 Console 线，完成现场基础操作；需要时，让远端同事或客户一起调试。

我做这个 App，是从弱电工程师的现场工作出发。有时只是查看接口状态、读取配置或做个简单调整，也要抱着笔记本在机柜之间跑。Net Tentacle 把这些基础操作放到手机上，再用语音输入和 AI 辅助，减少打字、查命令和切换工具的麻烦。

适合弱电工程师、初级 IT 交付人员、网络运维，以及经过培训并获得授权的值班人员。复杂故障和配置变更仍需要相应的技术经验。

**0.2.0：远程协助与终端稳定性更新。安装包与更新说明见 [v0.2.0 Release](https://github.com/radeonbm/Net-Tentacle/releases/tag/v0.2.0)，文件名为 `Net-Tentacle.apk`。**

## 手机上能做什么

- **连接设备：** Android 8.0 及以上、支持 OTG / USB Host 的手机，配兼容的 USB 串口 Console 线。提供 Cisco、华为、H3C、锐捷参数预设，具体型号和线材需验证。
- **本地终端：** 登录设备、输入命令、查看真实回显，读取配置并保存本地备份。普通模式不开放自由终端输入，专家模式可手动操作。
- **语音描述需求：** 在“AI 配置”页用系统语音识别填写需求，核对接口名、VLAN 和数字后再生成；不是语音直接执行命令。
- **AI 辅助：** 解释配置和命令，根据当前配置与需求生成建议、查看差异；核对后确认下发，AI 批量下发流程保存修改前备份。
- **远程协助：** 现场手机接线，远端使用浏览器查看终端或输入命令，支持只读、协助和限时托管。

## 本地使用

**升级说明：** 0.2.0 关闭 APK 调试功能，应用名称不带 Debug；沿用旧公开版签名与包名，旧公开版可覆盖升级，建议先备份重要数据。内部测试包若为 `com.networkai.console.debug`，会与正式包并存，不会自动迁移设置。为保持兼容，本版保留历史 Android Debug 证书，并未更换为专用发布证书。

1. 从本项目 [Releases](https://github.com/radeonbm/Net-Tentacle/releases) 获取安装包，按 Android 提示安装。
2. 手机接 Console 线，进入“接入”，授权 USB，选择设备类型和串口参数。
3. 登录设备，先查询状态或读取当前配置；需要手动输入时开启专家模式。
4. 需要 AI 时配置所在组织允许使用的模型服务，再审阅配置或描述需求，核对建议后操作。

本地 Console 不依赖设备管理 IP 或互联网；AI、系统语音服务和远程协助的联网条件分别取决于所用服务。配置会按规则过滤敏感字段，但发送前仍要检查业务信息。

## 远程协助怎么用

现场人员只需手机接好 Console，IT 交付同事或客户就能在远端调试自己有权管理的设备，不用专门到场，也少一些拍照和转述。

1. **现场准备：** 确认手机本地 Console 能正常操作，手机和远端电脑均可联网。
2. **手机创建：** 开启专家模式，点击“终端”标题右侧的“远程协助”，选择模式，创建一次性邀请码。
3. **电脑加入：** 打开 [远程终端](https://remote.net-tentacle.cn/)，输入邀请码，填写称呼和接头暗号，把暗号告知现场人员核对。
4. **现场批准：** 手机核对对方身份、暗号和权限后批准。批准前，网页不能查看终端输出或操作设备。
5. **协同操作：** 只读模式查看回显；控制模式显示“已获得终端控制权限”，支持完整终端交互，包括输入、退格、Tab 补全和历史命令。
6. **结束：** 手机点“结束协助”或网页退出当前会话。需要继续时重新创建邀请并批准。

| 模式 | 远端可以做什么 | 时长 |
| --- | --- | --- |
| 只读查看 | 查看终端输出，不能输入 | 默认 2 小时 |
| 协助模式 | 现场批准后使用完整交互终端 | 默认 2 小时 |
| 限时托管 | 现场批准后，在选定时间内使用完整交互终端 | 手机选择时长或自定义 |

时长从**创建会话**开始计算，网页显示剩余时间，网页不能自行延长。协助和限时托管授予的是终端控制权限，**不是逐条命令审批**；可以修改配置等，请把权限交给已核对身份和操作范围的人。

### 断开后会怎样

- 电脑主动退出：手机提示远端用户已断开；手机结束：网页弹窗提示现场端已结束会话。
- 拔 Console 线：网页弹窗提示设备断开并停止输入。重新插线后，在手机点击一次“连接”；若会话未结束、网络正常且授权有效，检查回显后继续。
- 任一端网络中断：检测到后结束旧会话；恢复网络也不能凭旧网页直接恢复控制，需要新邀请和批准。本轮手机与电脑断网实测均约 10 秒提示，实际耗时随网络和系统调度变化。
- 到期：自动结束远程；手机的本地 Console 不因远程结束而断开。物理拔线时，本地串口当然也会断开。
- 会话中点击手机通知应返回当前终端，不重新创建远程连接。

## 使用边界与反馈

本轮测试中曾有一次闪退反馈，目前原因尚未确认，不宣称已修复。若再次遇到，请保留复现步骤，可从“设置 → 提交 Bug”手动提交本地诊断；不会自动发送邮件。设备与线材兼容性仍需按实际组合确认。

AI 建议下发与完整交互终端是两条不同路径：前者有建议核对、风险检查和备份流程；后者按键直接传给设备，不承诺逐条拦截危险命令，也不应当作完整的命令审计系统。

远程服务中转临时会话，不将终端内容写入服务日志或磁盘。终端回显会呈现给获准的远端人员，不等于 AI 外发时的脱敏内容；只向可信且获得授权的人共享。

反馈问题时，请说明手机型号、Android 版本、Console 线/芯片、设备型号与复现步骤，不要公开密码、密钥或真实设备配置。联系：bam.ming3@vnet.com。

## English

Net Tentacle combines an Android phone and a compatible OTG Console cable for on-site network-device checks, configuration review and manual operation. Voice input fills a requirement field; AI helps explain configurations and draft changes for human review, not automatic execution.

Version **0.2.0** adds browser-based remote assistance and terminal stability improvements. Download `Net-Tentacle.apk` and read the notes in [the v0.2.0 release](https://github.com/radeonbm/Net-Tentacle/releases/tag/v0.2.0).

### Remote workflow

1. Connect and verify the local Console. Both the phone and remote computer need network access.
2. Enable expert mode on the phone, open Remote Assistance beside the Terminal heading, choose a mode and create an invitation.
3. The guest opens [the remote terminal](https://remote.net-tentacle.cn/), enters the invitation and a name/access phrase. The on-site user verifies and approves the request.
4. Read-only sessions reject input. Assisted and timed-unattended sessions grant full interactive control, including Backspace, Tab and command history. This is **session authorization, not per-command approval or dangerous-command filtering**.
5. Read-only and assisted sessions default to two hours; timed mode allows a duration selection. The timer starts at creation. Either side may end the session; network loss and expiry also end authorization. A new invitation and approval are required after the session ends.

Unplugging Console disables remote input. After plugging it back in, tap Connect on the phone; remote operation can continue only while the session and its authorization remain valid. Phone and computer network-loss notifications each took about ten seconds in field testing; actual timing varies. Ending remote access does not disconnect an otherwise-connected local Console. The relay does not write terminal content to logs or disk; approved guests can see the actual terminal output.

One crash was reported during testing and remains undiagnosed. This version does not claim to fix it. Reports are sent manually by the user, never automatically.

Use only on authorized devices. Choose an approved AI service, review outgoing information and check generated commands before sending. Compatibility depends on the phone, serial adapter and network device.
