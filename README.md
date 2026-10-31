# HIK-Sense
海康4117超分软件
售后QQ群：672819936

本仓库仅用于发布 App 安装包。

## 最新版本：1.0.33（v49）

发布日期：2026-10-31

[下载最新安装包](https://github.com/beilusm/HIK-Sense/releases/download/v1.0.33/HIK-Sense-1.0.33-v49-release.apk) · [最新发布](https://github.com/beilusm/HIK-Sense/releases/latest) · [历史版本](https://github.com/beilusm/HIK-Sense/releases) · [更新日志](CHANGELOG.md)

更新日志：

- 新增应用内检查更新：启动时检查新版本；关于页顶部版本标签支持手动检查、查看更新日志和下载安装包，可忽略本次版本提醒。
- 更新下载接入六条 HTTPS 代理线路，按当次短样本自动选线，失败时切换备用线路；实际速度取决于网络和代理可用性。
- 记住 AI 超分模式（关闭、效果优先、性能优先），重新进入应用时恢复上次选择；性能优先遇到彩色调色板时提示切换白热或黑热。
- 新增跟随系统、浅色和深色三种明暗模式并保存选择，系统栏图标同步适配。
- 连接相机后补齐发射率读取，与原有画质参数一起回读设备当前值，避免把手机默认值误当成相机设置。
- 完善全屏操作：增加清除手动点/ROI 标注，显示录屏状态与计时，并修正全屏入口按钮边框裁切。
- 优化故障日志摘要的保留与生成流程：优先保留 AI 后端和异常线索，OTA 日志独立保存，常规逐帧成功消息改为计数摘要。

详细说明和限制见[本版发布说明](releases/v1.0.33/notes.md)。历史正式版 1.0.32 尚未接入应用内更新，首次请通过下载链接手动覆盖安装；1.0.33 起包含应用内更新。

## 软件检查更新的固定接口

软件始终请求同一个地址，即可取得最新正式版、更新日志与安装包下载地址：

```text
https://github.com/beilusm/HIK-Sense/releases/latest/download/latest.json
```

字段说明和后续发布流程见[发布规范](docs/releasing.md)。客户端以整数 `versionCode` 判断是否需要更新。

GitHub 标准最新版 API：

```text
https://api.github.com/repos/beilusm/HIK-Sense/releases/latest
```

每个正式版本使用独立标签 `v<versionName>` 和独立 Release；安装包仅作为对应 Release 附件发布。
