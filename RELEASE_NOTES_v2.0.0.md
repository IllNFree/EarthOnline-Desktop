# 地球Online Desktop（Windows）· v2.0.0 发布说明

## 版本定位

暂停端。本端最新基线为 v1.0.5（最后提交 2026-10-01）。v2.0.0 未在本端发布，本文件为跨端发版文档占位，待未来同步或安全修复时填充。

## 亮点

无（本端暂停维护）。最新可用能力见 v1.0.5 基线：WPF + MVVM、EF Core + SQLite 本地数据库、WebDAV 备份、回收站软删除、AI 对话与本地推理接入。

## 破坏性变更

无。

## 升级指引

暂停维护，不提供升级路径。当前用户停留在 v1.0.5；如需迁移数据，请用应用内 WebDAV 备份导出后导入其他活跃端。

## 已知问题

- 本端冻结于 v1.0.5，不再接收功能更新。
- 根目录散落文件夹（Assets / Converters / Data / Dialogs / Docs / EarthOnline-Setup / Migrations / Pages 等）待整理，见 `docs/root-cleanup-plan.md`（仅计划，未执行 git mv）。

## 完整变更

后续由 git-cliff 基于 Conventional Commits 自动生成并维护于 `CHANGELOG.md`。
