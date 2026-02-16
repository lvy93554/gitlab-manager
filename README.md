# gitlab-manager

一个用于操作gitlab的自动化工具

## 关于配置管理
📊 优先级排序(国际化标准实践)
标准优先级顺序(从高到低)
```shell
1. 命令行参数(最高优先级)
2. 环境变量
3. .env 文件
4. 配置文件(YAML/JSON/TOML)
5. 默认值(最低优先级)
```

### 为什么这样排序?
12-Factor App 方法论:

✅ 环境变量 > 配置文件
✅ 运行时配置 > 构建时配置
✅ 动态配置 > 静态配置

原因:
```shell
1. 环境变量:部署时设置,不同环境不同值,最灵活
2. .env 文件:本地开发时使用,不提交到版本控制
3. 配置文件:通用配置,可以提交到版本控制
4. 默认值:兜底配置,确保程序能运行
```

### 🔧 .env 文件在大型项目中的适用性
✅ .env 文件的优点

#### 本地开发友好

```shell
# .env 文件
   GITLAB_TOKEN=glpat-local-dev-token
   GITLAB_URL=https://gitlab-dev.company.com
   LOG_LEVEL=DEBUG
```

#### 敏感信息不提交

```shell
# .gitignore
   .env
```

#### 环境切换方便

```shell
.env.development
.env.staging
.env.production
```

### ⚠️ .env 文件的局限

#### 1. 不适合容器化部署

- Docker/K8s 使用环境变量或 Secret
- .env 文件需要额外挂载


#### 2. 不适合多实例部署

- 每个实例需要自己的 .env
- 不如集中配置管理

#### 3. 安全性考虑

- 文件权限管理复杂
- 容易误提交到版本控制



## 📋 大型项目推荐方案

# 大型项目推荐方案

| 场景        | 推荐方式             | 原因                           |
|-------------|----------------------|--------------------------------|
| 本地开发    | .env 文件            | 方便快捷                       |
| CI/CD       | 环境变量             | 平台原生支持                   |
| Docker      | 环境变量             | docker run -e                  |
| Kubernetes  | Secret / ConfigMap   | 原生支持，安全                 |
| 生产环境    | Secret 管理工具       | Vault, AWS Secrets Manager 等  |


## 🏆 国际化规范化配置方案
### .env 在大型项目中的适用性
# 配置管理方案对比

| 场景        | 使用 .env | 推荐方案                |
|-------------|-----------|-------------------------|
| 本地开发    | ✅ 推荐   | .env 文件               |
| Docker      | ❌ 不推荐 | 环境变量 -e             |
| Kubernetes  | ❌ 不推荐 | Secret + ConfigMap      |
| 生产环境    | ❌ 不推荐 | Secret 管理工具          |


## 关于环境变量
```shell
- APP_LOG_LEVEL: 项目的日志等级。通常分为：DEBUG、INFO、WARNING、ERROR、CRITICAL
```
