# 量潮DevOps发布管理章程

**第一条 制定依据**
本章程依据《量潮DevOps章程》制定，旨在建立版本发布的标准流程和规范。

**第二条 适用范围**
本章程适用于量潮科技所有仓库的版本发布。发布工具的使用方法见 DevOps 手册。

**第三条 发布流程**
版本发布按以下步骤执行：

（一）更新版本号。更新配置文件中的版本号。

（二）更新 CHANGELOG。在 `CHANGELOG.md` 中添加当前版本的变更记录，格式遵循 Keep a Changelog 规范。

（三）打标签。创建 git tag 标记发布版本。标签格式为 `vX.Y.Z`（单组件项目）或 `scope/vX.Y.Z`（多组件项目，如 `cli/v0.6.0`）。

（四）发布。创建 GitHub Release，Release body 须包含该版本的 CHANGELOG 内容。

**第四条 版本号规则**
版本号遵循语义化版本规范（SemVer）。正式版格式为 `vX.Y.Z`，预发布版在版本号后加 `-rc.N`、`-alpha.N`、`-beta.N` 等后缀。

Scope 前缀用于单仓多组件项目，对应 `.quanttide/devops/contract.yaml` 中定义的作用域。

**第五条 CHANGELOG 规则**
每个版本须在 `CHANGELOG.md` 中有对应条目。变更按 Added、Changed、Fixed、Removed 分类。CHANGELOG 由发布工具自动生成，发布前可人工修正。

**第六条 发布前检查**
发布前须确认最新标签与配置文件版本一致、CHANGELOG 条目存在、GitHub Release body 与 CHANGELOG 同步、工作区干净。

**第七条 回滚**
发布流程中任一步骤失败视为本次发布失败。标签推送失败时删除本地标签，GitHub Release 创建失败时删除本地和远程标签。修复问题后重新执行发布。

**第八条 附则**
本章程由 DevOps 团队负责解释和修订。各项目可制定子章程补充本项目特定的发布规则。
