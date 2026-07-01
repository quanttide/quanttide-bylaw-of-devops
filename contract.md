# 量潮DevOps契约章程

**第一条 制定依据**
本章程依据《量潮DevOps章程》制定，旨在定义单仓多组件项目的作用域管理规范。

**第二条 适用范围**
本章程适用于使用 tag 前缀区分多组件的单仓库项目（monorepo）。

**第三条 作用域定义**
作用域（Scope）通过 `.quanttide/devops/contract.yaml` 文件定义。每个作用域对应一个 tag 前缀和一组子目录，用于按组件独立管理版本发布。

**第四条 契约文件格式**
`.quanttide/devops/contract.yaml` 采用以下格式：

```yaml
# 作用域（tag 前缀）到子目录的映射
scopes:
  <scope名称>: <子目录路径>
```

scope 名称即 tag 前缀。子目录路径相对于仓库根目录。支持多层目录（如 `src/cli`）。

示例：

```yaml
# 单作用域
scopes:
  cli: .

# 多作用域（monorepo）
scopes:
  cli: src/cli
  studio: src/studio
  provider: src/provider
```

不带 scope 前缀的 tag（如 `v0.1.0`）默认属于根作用域，无需在配置中声明。

**第五条 作用域划分原则**
每个可独立发版的组件应声明为一个作用域。作用域划分以组件的发布频率和独立版本号为标准。不同作用域的版本号互不影响。

**第六条 附则**
本章程由 DevOps 团队负责解释和修订。各项目的 `contract.yaml` 配置对应具体作用域定义。
