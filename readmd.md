golang测试项目说明：

## debug说明

### 普通文件debug
https://github.com/golang/vscode-go/blob/master/docs/debugging.md#snippets

### 测试文件debug
注意项目如果是符号链接到 go/src 文件夹，测试文件debug会找不到文件，创建不了breakpoint(通过配置launch.json的test模式加上log发现此问题)

### 普通多main文件
在 go/src 目录下打开，vscode会报错，这是golang语言特情，目前无合适方法
在 符号链接目录 下不报

### 测试文件注意
1. xxx_test.go 为文件名
2. 测试方法同目录下，不同文件也不能重名
3. debug test 和 run test输出内容不一致，debug较详细
    run模式详细输出和避免cache的设置: "go.testFlags": ["-count=1","-v"],

### 改造原有联系过程
1. 直接改造 -> xxx_test.go 但package main还是报一堆错
2. 建origin目录，再迁移
3. 同一目录下文件package声明必须一致

### TIPS:
1. 所有的函数默认都是同目录/包可见的，不可重名，变量也是 -> TODO: 如何禁止?
2. 普通类库用Testing练习，只有客户、服务器需要创建比较多的测试目录
3. 关闭buildOnSave

### gui调试:
1. fyne和qt都要求在自己的main文件运行，所以需要创建多个目录, webview目前看似不需要
2. 直接调试go文件，qt和fyne的编译时间都很长, 可以先build, 创建独立的launch选项解决
https://github.com/therecipe/qt 调试编译时间过长
https://github.com/fyne-io/fyne 调试编译时间稍短，但也长
3. build已创建tasks,ctr+shift+b

### git忽略可执行文件
https://stackoverflow.com/questions/5711120/gitignore-without-binary-files