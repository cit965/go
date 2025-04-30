# 03-连接 mysql

### 一、前言

go-zero 是一款高效、易用的微服务框架，其内置的代码生成工具 `goctl` 能大幅提升开发效率。本教程将详细讲解如何在 go-zero 项目中集成 MySQL 数据库。

### 二、环境准备

1. **安装依赖工具**
   * **Go 1.16+**:&#x20;
   *   **MySQL 5.7+**: 推荐使用 Docker 快速部署：

       bashCopyDownload

       ```
       docker run --name mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d mysql:8.0
       ```
   *   **go-zero 工具链**:

       bashCopyDownload

       ```
       go install github.com/zeromicro/go-zero/tools/goctl@latest
       ```
2. 创建示例数据库

```sql
CREATE TABLE `user` (
                        `id` bigint unsigned NOT NULL AUTO_INCREMENT,
                        `name` varchar(255)  NOT NULL DEFAULT '' COMMENT '用户姓名',
                        `gender` tinyint(3) unsigned NOT NULL DEFAULT '0' COMMENT '用户性别',
                        `mobile` varchar(255)  NOT NULL DEFAULT '' COMMENT '用户电话',
                        `password` varchar(255)  NOT NULL DEFAULT '' COMMENT '用户密码',
                        `create_time` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
                        `update_time` timestamp NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
                        PRIMARY KEY (`id`),
                        UNIQUE KEY `idx_mobile_unique` (`mobile`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8mb4;
```

### 三、配置mysql 数据源

1.  **修改项目配置文件**\
    在 `etc/demo-api.yaml` 中添加 MySQL 配置：

    yamlCopyDownload

    ```
    Name: demo-api
    Host: 0.0.0.0
    Port: 8888
    Mysql:
      DataSource: root:123456@tcp(localhost:3306)/demo?charset=utf8mb4&parseTime=true
    ```
2.  **解析配置结构体**\
    在 `internal/config/config.go` 中定义配置：

    goCopyDownload

    ```
    package config

    import "github.com/zeromicro/go-zero/rest"

    type Config struct {
        rest.RestConf
        Mysql struct {
            DataSource string
        }
    }
    ```

### 四、生成模型代码

&#x20;使a用f `gasd octl` 自动生成数据库操作代码，大幅减少手写 SQL 的工作量：

```
goctl model mysql ddl -src .\model\user.sql -dir .\model
```

生成后的代码结构如下：

```
model/
├── user.sql
├── usermodel.go     # 自动生成的 CRUD 方法
└── vars.go          # 数据库连接配置
```

\
