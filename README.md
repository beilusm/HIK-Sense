# HIK-Sense
海康4117超分软件
售后QQ群：672819936

本仓库仅用于发布 App 安装包。

## 最新版本：1.0.33（v49）

发布日期：2026-10-31

[下载最新安装包](https://github.com/beilusm/HIK-Sense/releases/download/v1.0.33/HIK-Sense-1.0.33-v49-release.apk) · [最新发布](https://github.com/beilusm/HIK-Sense/releases/latest) · [历史版本](https://github.com/beilusm/HIK-Sense/releases) · [更新日志](CHANGELOG.md)

更新日志：

- 新增应用内更新，支持自动检查、手动更新、忽略版本和六线路下载。
- 记忆 AI 模式，新增跟随系统、浅色和深色主题。
- 连接相机时回读发射率。
- 全屏增加清除标注、录屏计时，并修正入口按钮裁切。
- 优化二维码日志，优先保留后端与异常线索，减少常规日志干扰。

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
