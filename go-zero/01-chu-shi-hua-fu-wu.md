# 01-初始化服务

之前一直是用的 b站出品的 kratos 框架来写微服务，最近开始学习 go-zero 框架，看看两个框架有什么不同。

首先我们需要安装一些必要的软件，在[ 官网安装页面](https://go-zero.dev/docs/tasks) 按照说明依次安装  golang ， goctl，protoc，go-zero （根据你电脑系统类型选择安装方式，linux，mac，windows 都支持）。

### 初始化一个简单的 http 服务

1. 新建一个文件夹，初始化项目： go mod init  helloworld
2. 创建两个文件 etc/helloworld.yaml  main.go , 内容如下：

```yaml
Name: HelloWorld.api
Host: 127.0.0.1
Port: 8080
```

```go
package main

import (
	"github.com/zeromicro/go-zero/core/conf"
	"github.com/zeromicro/go-zero/rest"
	"github.com/zeromicro/go-zero/rest/httpx"
	"log"
	"net/http"
)

func main() {
	var restConf rest.RestConf
	conf.MustLoad("etc/helloworld.yaml", &restConf)
	s, err := rest.NewServer(restConf)
	if err != nil {
		log.Fatal(err)
		return
	}

	s.AddRoute(rest.Route{ // 添加路由
		Method: http.MethodGet,
		Path:   "/hello/world",
		Handler: func(writer http.ResponseWriter, request *http.Request) { // 处理函数
			httpx.OkJson(writer, "Hello World!")
		},
	})

	defer s.Stop()
	s.Start() // 启动服务
}

```

3. 执行 go mod tidy 下载依赖
4. 启动服务

<figure><img src="../.gitbook/assets/1745829909946.png" alt=""><figcaption></figcaption></figure>

5. 打开浏览器，访问接口

<figure><img src="../.gitbook/assets/1745829991723.png" alt=""><figcaption></figcaption></figure>
