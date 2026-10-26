# Desktop 根目录清理计划（仅计划，未执行）

本文件记录 EarthOnline-Desktop 根目录散落文件夹向结构化布局迁移的计划。**仅输出计划，不执行任何 `git mv`**，由人工审核后操作。

## 现状

根目录同时存在源码、构建产物、文档与发行包，层次不清：

```
EarthOnline-Desktop/
├── App.xaml / App.xaml.cs
├── AssemblyInfo.cs
├── MainWindow.xaml / MainWindow.xaml.cs
├── global.json
├── Assets/                  # WPF 资源
├── Converters/  Data/  Dialogs/  Migrations/  Pages/  Services/  ViewModels/   # 源码
├── Docs/                    # 内部文档
├── EarthOnline-Setup/        # 安装工程
├── EarthOnline-SetupRelease/
├── EarthOnline-win-x64-v1.0.1.zip / EarthOnline-win-x64-v1.0.2.zip
├── publish/  publish-single/  publish_win/
├── RELEASE_NOTES_v1.0.2.md
├── VERIFICATION_CHECKLIST_v1.0.1.md
├── open_vs.bat  run.bat
├── EarthOnline-Desktop.csproj  EarthOnline-Desktop.slnx
└── Backups/
```

## 目标布局

```
EarthOnline-Desktop/
├── src/                      # 全部源码
│   ├── App.xaml(.cs)  AssemblyInfo.cs  MainWindow.xaml(.cs)  global.json
│   ├── Assets/  Converters/  Data/  Dialogs/  Migrations/
│   ├── Pages/  Services/  ViewModels/
├── build/
│   └── EarthOnline-Setup/     # 安装工程（原 EarthOnline-Setup/ + EarthOnline-SetupRelease/）
├── artifacts/                # 发行包与发布输出
│   ├── EarthOnline-win-x64-v1.0.1.zip
│   ├── EarthOnline-win-x64-v1.0.2.zip
│   └── publish/  publish-single/  publish_win/
├── docs/                     # 文档（原 Docs/ + 根级文档）
│   ├── RELEASE_NOTES_v1.0.2.md
│   └── VERIFICATION_CHECKLIST_v1.0.1.md
├── EarthOnline-Desktop.csproj
├── EarthOnline-Desktop.slnx
├── open_vs.bat  run.bat
├── .gitignore
├── LICENSE
└── README.md
```

## 迁移映射表

| 源路径（根目录） | 目标路径 | 类型 | 说明 |
| --- | --- | --- | --- |
| `App.xaml` `App.xaml.cs` `AssemblyInfo.cs` `MainWindow.xaml(.cs)` `global.json` | `src/` | 源码 | 入口与全局配置 |
| `Assets/` | `src/Assets/` | 源码 | WPF 资源，随源码编译 |
| `Converters/` `Data/` `Dialogs/` `Migrations/` `Pages/` `Services/` `ViewModels/` | `src/` 同名子目录 | 源码 | 直接平移 |
| `Docs/` | `docs/` | 文档 | 内部文档下挂 docs |
| `RELEASE_NOTES_v1.0.2.md` `VERIFICATION_CHECKLIST_v1.0.1.md` | `docs/` | 文档 | 根级文档归位 |
| `EarthOnline-Setup/` `EarthOnline-SetupRelease/` | `build/EarthOnline-Setup/` | 工程 | 安装工程集中到 build |
| `EarthOnline-win-x64-*.zip` | `artifacts/` | 发行包 | 历史发行包归档 |
| `publish/` `publish-single/` `publish_win/` | `artifacts/` | 构建输出 | 发布产物归档 |
| `Backups/` | `artifacts/Backups/` 或删除 | 杂项 | 本地备份，建议移出仓库或归档 |
| `EarthOnline-Desktop.csproj` `EarthOnline-Desktop.slnx` | 根目录 | 工程文件 | 保持根目录 |
| `open_vs.bat` `run.bat` | 根目录 | 脚本 | 保持根目录 |

## 人工审核清单（执行 git mv 前）

- [ ] 确认 `*.csproj` / `*.slnx` 中的相对引用路径在迁移后仍正确（如 `<Compile Include>`、`<Page Include>`、链接资源）。
- [ ] `App.xaml` 的 `StartupUri` / 资源字典路径随 `src/` 迁移后需相应调整。
- [ ] `Assets/` 内图片、字体等嵌入资源（Build Action）路径需复检。
- [ ] `EarthOnline-Setup/` 引用的主输出路径（指向 `src/` 编译结果）需更新。
- [ ] 迁移后执行一次 `dotnet build` 验证可编译、可发布。
- [ ] `git mv` 逐目录执行并单次提交，便于回溯；勿一次性大范围移动。
- [ ] 本端处于暂停维护，本次清理非紧急；建议并入下一次安全修复一并处理。
