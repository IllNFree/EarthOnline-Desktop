# 地球Online · Desktop（Windows）

![Platform](https://img.shields.io/badge/platform-Windows-WPF-0078D4) ![Version](https://img.shields.io/badge/version-v2.0.0-lightgrey) ![License](https://img.shields.io/badge/license-MIT-green)

同名应用的 Windows 桌面端，WPF 实现。

## 当前状态

暂停维护，基线 v1.0.5，最后提交 2026-10-01。

v1.0.5 之后仅接收安全修复，不主动发版。发布流水线（`release.yml`）保留用于未来安全补丁。根目录散落文件夹的整理计划见 [Docs/root-cleanup-plan.md](Docs/root-cleanup-plan.md)。

## 技术栈

- WPF + MVVM
- Entity Framework Core + SQLite（本地数据库）
- .NET 8（net8.0-windows）
- 原生桌面，无第三方 UI 框架

## 跨端契约

四端共用同一份数据契约 `earth_online_backup.json`：字段全 camelCase、WebDAV 按主键合并、软删除对齐。完整契约见 Web 仓库 [docs/contract.md](https://github.com/IllNFree/EarthOnline-Web/blob/main/docs/contract.md)。

## 快速开始

暂停维护，不提供新构建指引。

## 仓库导航

- Web（PWA）：https://github.com/IllNFree/EarthOnline-Web
- Android：https://github.com/IllNFree/EarthOnline-Android
- iOS：https://github.com/IllNFree/EarthOnline-iOS

## 许可证

[MIT](LICENSE)
