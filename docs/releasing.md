# 发布与更新接口规范

## 仓库结构

```text
README.md
CHANGELOG.md
docs/releasing.md
releases/
  v1.0.31/notes.md
  v1.0.32/
    notes.md
    latest.json
```

Git 仅保存发布说明、更新元数据和规范。APK 放在 GitHub Release 附件中，不放进 Git。
版本标签标记发布元数据提交，并非应用源码提交；应用源码在独立仓库管理。

## Release 约定

- 一个正式版本对应一个标签 `v<versionName>`，例如 `v1.0.32`。
- 标题统一为 `HIK-Sense <versionName>`，正文使用该版本 `notes.md`。
- 每个 Release 仅包含本版本 APK 和 `latest.json`；历史迁移版 v1.0.31 保留原 APK 与说明。
- APK 文件名为 `HIK-Sense-<versionName>-v<versionCode>-release.apk`。
- 已发布版本不改号、不移动标签、不替换原 APK；新版本建立新的 Release。
- 只有完整上传并核对附件后，才能发布并显式标记最新稳定版；草稿/预发布不作为最新正式版。
- 不再使用共用的 `app` 标签混放不同版本。

## 客户端固定地址

```text
https://github.com/beilusm/HIK-Sense/releases/latest/download/latest.json
```

每个新 Release 都上传文件名完全相同的 `latest.json`，因此软件中的请求地址无需随版本变化。
客户端需允许 HTTPS 重定向；该地址最终返回 JSON。缓存可能短暂保留旧版本信息。

| 字段 | 类型 | 含义 |
| --- | --- | --- |
| schemaVersion | integer | 接口结构版本，当前为 1 |
| applicationId | string | Android 包名 |
| versionName | string | 展示版本，例如 1.0.32 |
| versionCode | integer | Android 内部版本号，例如 48；用于更新比较 |
| releaseDate | string | 发布日期，YYYY-MM-DD |
| minSdkVersion | integer | 最低 Android API 级别 |
| changelog | string[] | 本版本面向用户的更新条目 |
| downloadUrl | string | 指向本版本 APK 的 HTTPS 固定下载地址 |
| releaseUrl | string | 本版本 Release 页面 |
| apkSize | integer | APK 字节数，用于展示和下载长度检查 |

客户端读取 JSON 后，仅当 `applicationId` 匹配且远端 `versionCode` 大于本机时提示更新；
显示 `versionName`、`changelog`，使用 `downloadUrl` 下载。不能按版本字符串字典序比较。
元数据和文件长度不构成应用授权依据；升级兼容性继续依赖 Android 包名、版本与原签名证书校验。
本仓库不提供 APK SHA 字段、不计算或比对整包 SHA、不发布 `.sha256` 文件。

也可直接使用 GitHub 标准 API：

```text
https://api.github.com/repos/beilusm/HIK-Sense/releases/latest
```

其中 `tag_name` 为版本标签，`body` 为 Markdown 更新日志，`assets` 为附件列表。
自定义 JSON 额外提供 `versionCode`、最低系统版本等 Android 更新需要的明确字段。

## 后续发布顺序

1. 取得用户对该批正式发布的明确授权，确认现有 APK 的版本、包名、原证书及静态检查记录。
2. 新增 `releases/v<versionName>/notes.md` 和 `latest.json`，更新 README 与 CHANGELOG。
   JSON 的更新条目与 Release 正文一致，下载地址使用本次独立版本标签。
3. 静态核对 JSON、版本/文件名/字节数、文档链接和提交范围；不执行应用功能测试。
4. 提交元数据到 `main`，创建对应版本标签，建立草稿 Release。
5. 上传唯一的该版本 APK 及该版本 `latest.json`，核对附件名称、大小和 uploaded 状态。
6. 发布正式 Release 并显式设为 latest；读取固定 JSON 地址和标准 latest API，核对返回同一版本。
7. 记录实际发布地址和提交；所有功能、升级和软件内检查更新的验收由用户执行。

官方地址规则：[固定最新版及附件链接](https://docs.github.com/en/repositories/releasing-projects-on-github/linking-to-releases)、
[最新版 API](https://docs.github.com/en/rest/releases/releases#get-the-latest-release)。
