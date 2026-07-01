# 发布管理章程

本文定义量潮 DevOps 的版本发布规范，所有项目的版本发布必须遵守此流程。

## 标准发布流程

每次发版本按以下步骤执行：

1. **更新版本号**：修改 `Cargo.toml` / `pyproject.toml` 中的 `version` 字段
2. **更新 CHANGELOG**：在 `CHANGELOG.md` 中添加当前版本的变更记录
3. **打标签**：创建 git tag（格式 `vX.Y.Z` 或 `scope/vX.Y.Z`）
4. **发布**：创建 GitHub Release，附 CHANGELOG 内容

上述流程已封装为一条命令：

```bash
qtcloud-devops release publish -v <version> -y
```

该命令自动完成步骤 1-4。

## 版本号格式

版本号必须遵循语义化版本规范（SemVer），格式为 `vX.Y.Z` 或 `scope/vX.Y.Z`。

正式版：`v1.0.0`、`cli/v0.6.1`
预发布版：`v0.6.0-rc.1`、`cli/v0.7.0-alpha.1`

Scope 前缀用于单仓多组件场景（如 monorepo），对应 `.quanttide/devops/contract.yaml` 中定义的作用域。

## CHANGELOG 规范

每个版本必须在 `CHANGELOG.md` 中有对应条目，格式：

```markdown
## [X.Y.Z] - YYYY-MM-DD

### Added
- 新功能描述

### Fixed
- 修复描述

### Changed
- 变更描述
```

CHANGELOG 由 `release publish` 自动生成（基于 git 提交记录，LLM 协助），发布前可人工修正。

## 发布前检查

每次操作开始和结束时执行：

```bash
qtcloud-devops release status
```

确认以下事项：
- 最新 tag 与配置文件版本一致
- CHANGELOG 条目存在
- GitHub Release body 与 CHANGELOG 同步
- 工作区干净

## 回滚

发布流程中任一步骤失败：
- 标签推送失败：自动删除本地标签
- GitHub Release 创建失败：自动删除本地和远程标签

状态不回退，修复问题后重新执行 `publish`。
