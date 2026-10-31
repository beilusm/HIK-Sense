# 发布仓库约定

这是安装包分发仓库；应用源码位于独立的 Hikvision-4117 仓库。
操作前阅读 README.md、CHANGELOG.md 和 docs/releasing.md，遵循版本目录与接口契约。

- 每版使用独立 `v<versionName>` 标签及 Release，不复用 `app`，不混放不同版本 APK。
- 软件固定读取 `https://github.com/beilusm/HIK-Sense/releases/latest/download/latest.json`。
  每个新正式 Release 必须附带该版本 APK 与同名 `latest.json`。
- Git 只保存说明、规范和元数据，不提交 APK、签名材料、客户数据或原始日志。
- 仅在用户明确授权当前批次后发布；整理已有批次不另行分配应用版本、不重编译或重签。
- 禁止计算或比对整包 APK SHA，禁止生成 APK 哈希文件；保留包名、版本、证书、ABI、R8 等静态检查。
- 用户亲自执行全部功能测试；代理仅作静态内容、文档、元数据与远端发布状态核对。
- 先草稿上传并检查，再发布并设为 latest。已发布版本不覆盖 APK，不移动版本标签。
- 更新日志必须和该版实际内容一致，不能将构建、静态检查或发布成功写成功能验收。
