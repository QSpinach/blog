---
tags: [npm,yarn]
comments: true
toc: true
---



### centos7 下安装nodejs

```
$ curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash
$ curl --silent --location https://deb.nodesource.com/setup_8.x | sudo bash
$ curl --silent --location https://deb.nodesource.com/setup_10.x | sudo bash


$ yum install -y nodejs
```
### nvm 安装node
根据提示设置nvm路径和nodejs路径
node下载源
```
nvm node_mirror https://npm.taobao.org/mirrors/node/
```
npm下载源
```
nvm npm_mirror  https://npm.taobao.org/mirrors/npm/
```

### 使用nvm下载node
```
nvm install 8.0.0 64-bit
nvm use 8.0.0
nvm list //查看以己经安装的

windows下的nvm命令
nvm arch                         查看当前系统的位数和当前nodejs的位数
nvm install <version> [arch]     安装制定版本的node 并且可以指定平台 version 版本号  arch 平台
nvm list [available]         
  - nvm list   查看已经安装的版本
  - nvm list installed 查看已经安装的版本
  - nvm list available 查看网络可以安装的版本
nvm on                           打开nodejs版本控制
nvm off                          关闭nodejs版本控制
nvm proxy [url]                  查看和设置代理
nvm node_mirror [url]            设置或者查看setting.txt中的node_mirror，如果不设置的默认是 https://nodejs.org/dist/
nvm npm_mirror [url]             设置或者查看setting.txt中的npm_mirror,如果不设置的话默认的是：https://github.com/npm/npm/archive/.
nvm uninstall <version>          卸载制定的版本
nvm use [version] [arch]         切换制定的node版本和位数
nvm root [path]                  设置和查看root路径
nvm version                      查看当前的版本
```
### NPM设置淘宝镜像
1. 查询当前配置的镜像
```
npm get registry
```
> https://registry.npmjs.org/

2. 设置成淘宝镜像
```
npm config set registry http://registry.npm.taobao.org/
```
3. 换成原来的
```
npm config set registry https://registry.npmjs.org/
```

### Yarn 设置淘宝镜像
1. 查询当前配置的镜像
```
yarn config get registry
```
> https://registry.yarnpkg.com

2. 设置成淘宝镜像
```
yarn config set registry http://registry.npm.taobao.org/
```

### 发布自己的包
1. 注册npm账号
2. 登录npm账号
`npm login` 找到需要发布的包根目录下
3. 发布包
`npm publish` 直接发布
4. 删除已发布的包
`npm unpublish 包名 --force` 
只能删除72小时内发布的包。删除的包，在24小时内不允许重复发布。发布包需谨慎，不要发布无意义的包。


### 解决的一些问题
1. @vue/cli 创建项目是安装chromedriver时失败的问题
此方法是单独安装chromdriver
```
npm install chromedriver --chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver
```
所以可以在给npm和yarn设置chromedriver源
设置
```
npm config set chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver
```
设置
```
yarn config set "chromedriver_cdnurl" "https://npm.taobao.org/mirrors/chromedriver"
```
2. The engine "node" is incompatible with this module. Expected version "=> ^4.0.0".
error Found incompatible module
```
yarn help | grep -- --ignore
    --ignore-scripts                  don't run lifecycle scripts
    --ignore-platform                 ignore platform checks
    --ignore-engines                  ignore engines check
    --ignore-optional                 ignore optional dependencies 
```
3. 关于node-sass不能安装问题
设置npm or yarn淘宝镜像源
```
npm config set sass-binary-site http://npm.taobao.org/mirrors/node-sass
```
指定node-sass下载源
```
yarn config set sass-binary-site http://npm.taobao.org/mirrors/node-sass
```

管理员身份运行cmd 安装
```
npm install -global -production windows-build-tools
```


