# 使用 kitex 来生成相关协议

```
    // 当前项目根目录执行
    kitex -type protobuf -module "kitex-proto/v1" -I ./ -I /Users/caoxl/go/src/github.com/gogo/protobuf ./MicroService/MicroService.proto 
```

其中 `-I /Users/caoxl/go/src/github.com/gogo/protobuf` 是示例里存放 `github.com/gogo/protobuf/gogoproto/gogo.proto` 的目录。

## 前置工作有:

```
    go env -w GO111MODULE=off
    
    go get github.com/gogo/protobuf/proto
    go get github.com/gogo/protobuf/gogoproto
    
    go env -w GO111MODULE=on
```

### Protobuf 文件生成 Go 文件命令

```
.proto 文件需要配置 option go_package="{go_package_path};{go_package_name}";
    generate_path: go文件路径，项目引入完整的目录。
    go_package_name: go 文件包名，需要与生成路径的目录保持一致。
    
service grpc 服务端go文件生成：
    protoc --go-grpc_out=paths=source_relative:. *.proto
    
客户端go文件生成：
    protoc --go_out=paths=source_relative:. *.proto
    
protoc 常用options说明
    --proto_path 指定使用到的外部proto文件路径
    --go_out 客户端go文件生成路径，'source_relative:.' 与proto源文件同一目录
    --go-grpc_out 服务端go文件生成生成路径，'source_relative:.' 与proto源文件同一目录
```