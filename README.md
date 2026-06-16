# 源流 WPS 智能助手 BYOK 版

**Sourceflower WPS AI Assistant** · v1.0.6 BYOK Edition

> 🏆 *Codex for Open Source applicant — bridging AI into China's 500M+ WPS Office ecosystem.*

轻量 WPS AI 助手：用户自行配置 [DeepSeek](https://www.deepseek.com/) API Key 后即可在 WPS 中对选中文本进行润色、总结、纠错等操作。本项目也是源流数字垂直领域 AI 工具的开发样板，便于参考 WPS 加载项与 BYOK 接入方式。

仓库地址：https://github.com/SourceFlowDigital/sourceflower-wps-assistant

---

## 项目定位

WPS Office 在中国拥有 **超过 5 亿用户**，但其 AI 插件生态几乎空白——Microsoft Office 有丰富的开源 AI 插件，而 WPS 开发者社区鲜有可参考的开源实现。本项目填补了这一空白：

- **面向普通用户**：一键安装，填入自己的 DeepSeek API Key 即可在 WPS 中使用 AI，无需编程
- **面向开发者**：提供完整的 WPS 加载项开发参考样板（BYOK 架构、本地安全存储、Ribbon UI 集成）
- **面向生态**：推动 WPS 办公场景下开源 AI 工具的普及，降低用户对海外闭源 AI 服务的依赖

由 **宁夏源流数字** 开源发布（Apache 2.0），持续维护。

---

## 功能特点

| 能力 | 说明 |
|------|------|
| 文本润色 | 优化表述，保持原意 |
| 文本总结 | 提炼要点 |
| 错别字 / 病句纠错 | 修正明显错误；无问题时不会用占位句敷衍 |
| 内容扩写 | 在选中内容基础上延展 |
| 内容改写 | 换种说法重写选中内容 |
| 续写 | 基于选中内容继续生成 |
| 缩写 | 精简文本 |
| 中英翻译 | 选中中文翻译为英文，反之亦然 |
| 语气转换 | 在正式、口语、商务等语气间切换 |
| 自定义回复长度 | 主界面可设字数上限，默认 300；留空或填 0 表示不限制 |
| 自填 DeepSeek API Key | 设置页保存后即可使用 |
| 本地保存 API Key | **仅存本机插件环境，不上传任何服务器** |
| WPS 插件形态 | 顶部「源流WPS助手」选项卡，选中文字后一键处理 |

---

## 适用场景

- 合同与政策类文稿**润色校对**
- 会议纪要**总结提炼**
- 错别字与病句**自动纠错**
- 段落扩写与改写
- 中英文快速互译
- 日常办公写作辅助

---

## 技术架构

```
WPS 加载项工程
├── manifest.xml          ← WPS 加载项注册清单
├── ribbon.xml            ← WPS 顶部选项卡 UI 定义
├── index.html            ← 插件主面板 UI
├── js/                   ← 业务逻辑（任务窗格通信）
├── ui/                   ← 设置界面
├── main.js               ← 入口
├── vite.config.js        ← 构建配置
└── release/              ← 打包后的安装包
```

- **BYOK 架构**：插件不含任何内置 AI 额度，API Key 仅存本机，请求直连 DeepSeek
- **隐私优先**：零服务器依赖，无数据采集，无埋点
- **构建工具**：Vite
- **安装方式**：一键 `install.bat`（含 WPS 注册表写入、加载项路径注册）

---

## 使用前准备

1. **Windows** 电脑（与当前安装包一致）
2. 已安装 **WPS Office**（文字组件）
3. 自备 **DeepSeek API Key**（[DeepSeek 开放平台](https://platform.deepseek.com/api_keys) 申请）
4. 下载本仓库 **Releases** 中的安装包 zip，解压到任意目录（路径建议不含特殊字符）

---

## 安装方法

1. 从 [GitHub Releases](https://github.com/SourceFlowDigital/sourceflower-wps-assistant/releases) 下载并解压安装包。
2. 进入解压目录，双击运行 **`install.bat`**。
3. 按提示保存并关闭 WPS 文档；在命令行输入 **`Y`** 并 **回车** 确认继续安装。
4. 等待提示「安装成功」后，重新打开 **WPS 文字**。
5. 确认顶部出现 **「源流WPS助手」** 选项卡 → 打开助手 → 在 **设置** 中填写并保存 **DeepSeek API Key**。
6. 配置完成后即可使用快捷按钮或「询问 DeepSeek」。

> 每次安装会生成新的安装标识；卸载后重新安装可能再次显示欢迎引导，一般不会清除您已保存的 API Key（以实机为准）。

---

## 卸载方法

1. 在安装包目录运行 **`uninstall.bat`**。
2. 按提示保存并关闭 WPS；输入 **`Y`** 并 **回车** 确认卸载。
3. 看到「卸载完成」后重新打开 WPS，确认 **「源流WPS助手」** 已消失。

卸载仅删除本插件目录与相关本地配置，不会清理 WPS 公共缓存或其他加载项。

---

## DeepSeek API Key 说明

- API Key 需您自行在 **DeepSeek 官方平台** 申请；插件 **不提供**、**不销售** API Key。
- 插件 **不包含** DeepSeek 模型额度；所有 AI 请求由插件在联网状态下 **直连 DeepSeek**。
- **调用费用** 由 DeepSeek 按您的账号规则计费，请自行关注余额与用量。
- API Key **仅保存在本机** 插件环境中，请勿向他人泄露；更换电脑需在新环境重新配置。
- 获取入口：https://platform.deepseek.com/api_keys

---

## 常见问题（FAQ）

### 插件不显示怎么办？

请 **完全退出 WPS**（任务栏无 WPS 图标）后重新打开。若仍无「源流WPS助手」，可右键 `install.bat` **以管理员身份运行** 后重装，或联系源流数字技术支持。

### 是否包含 DeepSeek 额度？

**不包含。** 本插件为 BYOK 模式，不内置、不赠送、不代扣 DeepSeek 额度。

### API Key 怎么获取？

登录 [DeepSeek 开放平台](https://platform.deepseek.com/api_keys)，按官方指引创建 API Key，复制到插件 **设置** 中保存即可。

### 为什么 AI 没有回复？

常见原因：未配置或 Key 无效、网络不可用、DeepSeek 账户余额不足、未选中文字且问题为空等。请先检查设置页 Key 状态与网络，并查看插件中的错误提示。

### 是否可以换电脑使用？

可以。在新电脑上安装插件后 **重新填写并保存** 您的 API Key 即可；旧机上的 Key 不会自动同步。

### 是否可以转发安装包？

安装包可按您的购买或使用支持约定自行备份与迁移；**请勿** 在公开场合分享您的 API Key。

### 如何卸载？

运行安装包目录中的 **`uninstall.bat`**，按提示 `Y` + 回车，完成后重启 WPS 检查选项卡是否已移除。

### AI 内容是否可靠？

AI 输出仅供参考，可能存在遗漏或错误。重要合同、政策、财务与对外材料请 **人工核验** 后再使用。

---

## 开发与构建（可选）

本仓库为 WPS 加载项前端工程。开发者可在克隆仓库后执行：

```bash
npm install
npm run build
```

产物用于打包进 `release` 安装目录；普通用户只需使用 **Releases 安装包**，无需本地构建。

---

## 贡献指南

欢迎提交 Issue 和 PR。贡献方向包括但不限于：

- 🐛 Bug 修复
- ✨ 新功能（更多 AI 模型支持、批量处理等）
- 📝 文档改进（安装说明、开发文档）
- 🌍 国际化（英文 UI 支持）
- 🔌 多模型适配（通义千问、文心一言等）

---

## 免责声明

- 本插件及 AI 生成内容 **仅供参考**，不构成法律、财务、投资、医疗或其他 **专业建议**。
- 用户应 **自行判断并核验** 所有输出内容，对采用 AI 结果后的后果自行负责。
- **DeepSeek API 调用费用** 由用户自行承担；请妥善保管 API Key，因泄露或误用产生的费用与风险由用户自行承担。
- 源流数字不对第三方模型服务的可用性、价格变更或内容准确性作担保。

---

## 许可证

Apache 2.0 © 2026 SourceFlowDigital · 宁夏源流数字服务有限公司

---

## 关于我们

[宁夏源流数字服务有限公司](https://sourceflower.com) 承接中小企业与个人 **垂直领域 AI 工具开发**，包括小程序、Web 工具、WPS / Office 插件、文档自动化、行业问答助手、测算工具等。

**主打低成本、快验证、能落地。**

- 官网：[sourceflower.com](https://sourceflower.com)
- GitHub：[github.com/SourceFlowDigital](https://github.com/SourceFlowDigital)
- 技术支持：sourceflowdigital@gmail.com
- 作者：润源

---

## 版本说明

当前版本：**v1.0.6 BYOK 纯净版** — 无插件内激活、无官方试用额度、无内置 AI 额度；用户自填 DeepSeek API Key 后使用。
