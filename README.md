# AWS Sam Docker Compose Example

This is an example of an application using AWS Sam to manage Lambda, API Gateway and DynamoDB. It is set up to run acceptance tests locally using Docker Compose to exercise the API from the outside.

## Running tests

To run acceptance tests against the app, run:

```shell
./test.sh
```

This creates 3 containers:

 - a local DynamoDb
 - the app itself, run with `sam local start-api`
 - the acceptance tests

The container running the app has the Docker socket on the host machine mounted inside it, as well as the current directory so that the Sam containers have access to the code. There is a step before the app starts where the `node_modules` directory is copied into the working directory - this is ensure that the dependencies installed are for Linux rather than whatever the host OS is.



AWS sam docker compose example
这个下载下来的代码有许多的坑点
1 DynamoDB需要设置为共享模式 最好设置一个卷映射 否则aws cli和workbench创建的数据互相看不见
2 配置一个局域网 大家可以互相访问 同一个网络大家可以互相访问 否则会timeout
3 自动测试刚开始不太懂 也很坑人
4 里面设定的$PWD是给linux用的  我修改成了window使用的格式了

该代码一共会启动3个常驻的Docker 启动第三个acceptance-test-1测试完成后会停掉 去看他的日志会显示测试结果
测试期间会有独立的容器创建出来进行测试 并且测试完毕以后会自动删除容器