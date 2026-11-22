# EnergyMind

**把整件事交给 Harness。** 收到客户投诉，在邮件里点「交给 Harness」。它可以从附件里找证据，调用 8D 质量技能，生成可编辑的 Word 报告，再帮你同步到飞书群、起草客户回信。前一步的结果直接用于下一步，整件事留在同一个会话里。

[下载 macOS 版](https://github.com/EugeneJian/EnergyMind-Releases/releases/latest) · [能力](#能力) · [使用指南](docs/user-guide.md) · [发行许可](https://github.com/EugeneJian/EnergyMind-Releases/blob/main/LICENSE)

5.2.16 Alpha · Apple 芯片 · macOS 14 及以上

![一封客户投诉交给 Harness，它调度 8D Quality Skill、办公工具、飞书和邮件，生成报告、同步质量群并起草回信](docs/media/harness-8d-workflow.png)

试用这个场景时，先启用自己的 8D Skill，连接邮箱和飞书。报告里可以标出已确认的事实和仍待验证的根因。你审阅后确认发到哪个群，给客户的回信在原邮件中核对、发送。 [按此场景试一次](docs/user-guide.md#从客户投诉到报告和回信)

## 能力

| 能力 | 在 EnergyMind 里怎么用 |
| --- | --- |
| **内置办公套件** | 把 PDF、Word、Excel 或 PowerPoint 直接交给 Harness 读取和分析。扫描 PDF 可按页交给支持图片输入的模型。结果可整理成可编辑的 Word、Excel 和 PowerPoint 文件。 |
| **飞书 · Lark** | 检查 Node.js、官方 `lark-cli` 的安装、配置及登录状态，可从应用启动官方安装和更新。Harness 可使用已安装并启用的飞书技能，按账号授权处理文档、多维表格、云盘、知识库、消息、日历和任务等。 |
| **邮件** | 通过 IMAP/SMTP 接入邮箱，可把邮件正文和附件一键交给 Harness 整理、起草回复。邮件缓存使用 AES-256-GCM 在本机加密，邮箱授权码存入系统钥匙串。 |
| **你的 Skill，你做主** | 让 Harness 把常用流程、脚本和模板做成 Skill。在「技能」里管理自己的 Skill，决定如何编辑、何时启用、恢复哪个版本。签名 macOS 版的「我的技能」可通过个人 iCloud 在多台 Mac 间同步。 |
| **专业工具** | 示波器读设备录波，支持双游标测量、积分和事件定位。可视化处理表格，支持分类汇总、筛选、下钻和出图。两者可单独打开，也可由 Harness 在同一任务中调用。 |
| **Runtime** | 随版本跟进 Pi，5.2.16 内置 Pi 1.6.0。Harness 已定义会话、事件和工具接口，计划通过适配器接入更多 Runtime。 |

### 个人数据与权限

对话、工作文件和生成结果默认保存在你的设备，录波和表格分析可离线完成。联网任务由本机直连对应服务，业务数据无需经 EnergyMind 服务器中转。使用在线模型时，本轮提问及任务所需的附件和工具结果会交给你选定的模型服务商。

Harness 默认在本机工作区执行任务。工作区外写入、管理员命令等受控操作触发工具检查时，Harness 会先请你确认。macOS「我的技能」通过同一 Apple 账户的专用 iCloud 容器同步，Apple 在传输和存储时加密。 [数据与安全](docs/user-guide.md#数据与安全) · [Apple 的 iCloud 数据安全说明](https://support.apple.com/en-us/102651)

## 把团队的做法留成 Skill

在 Harness 里说「把刚才的投诉处理流程保存为技能」，核对报告模板和处理步骤，下次可以直接复用。团队发布的云端技能会自动同步。 [技能管理与版本恢复](docs/user-guide.md#管理和同步技能)

## 同一个 Harness 也能完成工程任务

![从逆变器 Excel 或 CSV 开始，Harness 调度示波器计算电量、可视化出图、办公工具生成 Word 周报，并衔接飞书群和邮件回复](docs/media/harness-engineering-workflow.png)

工程师可以从会话中的事件明细回到原始录波，用双游标复核功率变化，再打开 Word 文件继续编辑。 [查看示波器复核示例](docs/media/scope-cursors.png)

[第三方组件与对应源码](THIRD-PARTY.md)
