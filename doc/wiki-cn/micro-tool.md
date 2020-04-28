# 介绍

micro包含了一批好用的工具集，比如项目一键生成、基于proto生成http&grpc代码，生成缓存回源代码，生成memcache执行代码，生成swagger文档等。

# 获取工具

执行以下命令，即可快速安装好`micro`工具
```shell
go get -u github.com/gs02048/micro/tool/micro
```

那么接下来让我们快速开始熟悉工具的用法~

# micro本体

`micro`是所有工具集的本体，就像`go`一样，拥有执行各种子工具的能力，如`go build`和`go tool`。先让我们看看`-h`的输出：

```
NAME:
   micro - micro tool

USAGE:
   micro [global options] command [command options] [arguments...]

VERSION:
   0.0.1

COMMANDS:
     new, n        create new project
     build, b      micro build
     run, r        micro run
     tool, t       micro tool
     version, v    micro version
     self-upgrade  micro self-upgrade
     help, h       Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --help, -h     show help
   --version, -v  print the version
```

可以看到`micro`有如：`new` `build` `run` `tool`等在内的COMMANDS，那么接下来一一演示如何使用。

# micro new

`micro new`是快速创建一个项目的命令，执行如下：

```shell
micro new micro-demo
```

即可快速在当前目录生成一个叫`micro-demo`的项目。此外还支持指定owner和path，如下：

```shell
micro new micro-demo -o YourName -d YourPath
```

注意，`micro new`默认会生成通过 protobuf 定义的`grpc`和`bm`示例代码的，如只生成bm请加`--http`，如下：

```shell
micro new micro-demo -o YourName -d YourPath --http
```

如只生成grpc请加`--grpc`，如下：

```shell
micro new micro-demo -o YourName -d YourPath --grpc
```

> 特别注意，如果不是MacOS系统，需要自己进行手动安装protoc，用于生成的示例项目`api`目录下的`proto`文件并不会自动生成对应的`.pb.go`和`.bm.go`文件。

> 也可以参考以下说明进行生成：[protoc说明](protoc.md)

# micro build & run

`micro build`和`micro run`是`go build`和`go run`的封装，可以在当前项目任意目录进行快速运行进行调试，并无特别用途。

# micro tool

`micro tool`是基于proto生成http&grpc代码，生成缓存回源代码，生成memcache执行代码，生成swagger文档等工具集，先看下的执行效果：

```
micro tool

protoc(已安装): 快速方便生成pb.go的protoc封装，windows、Linux请先安装protoc工具 Author(micro) [2019/10/31]
genbts(已安装): 缓存回源逻辑代码生成器 Author(micro) [2019/10/31]
testcli(已安装): 测试代码生成 Author(micro) [2019/09/09]
genmc(已安装): mc缓存代码生成 Author(micro) [2019/07/23]
swagger(已安装): swagger api文档 Author(goswagger.io) [2019/05/05]

安装工具: micro tool install demo
执行工具: micro tool demo
安装全部工具: micro tool install all
全部升级: micro tool upgrade all

详细文档： https://github.com/gs02048/micro/blob/master/doc/wiki-cn/micro-tool.md
```

> 小小说明：如未安装工具，第一次运行也可自动安装，不需要特别执行install

目前已经集成的工具有：

* [micro](micro-tool.md) 为本体工具，只用于安装更新使用；
* [protoc](micro-protoc.md) 用于快速生成gRPC、HTTP、Swagger文件，该命令Windows，Linux用户需要手动安装 protobuf 工具；
* [swagger](micro-swagger.md) 用于显示自动生成的HTTP API接口文档，通过 `micro tool swagger serve api/api.swagger.json` 可以查看文档；
* [genmc](micro-genmc.md) 用于自动生成memcached缓存代码；
* [genbts](micro-genbts.md) 用于生成缓存回源代码生成，如果miss则调用回源函数从数据源获取，然后塞入缓存；

-------------

[文档目录树](summary.md)