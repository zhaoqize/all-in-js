> Node.js v8.11.1
> NPM v5.6.0

## NPM 包安装

安装的版本默认是`latest`

```js
npm install <package-name> [--save-prod] (npm install <package_name>) // 安装在dependenies
npm install <package-name> [--save-dev] // 安装在devDependenies
npm install @scope/package-name // 安装公开包
npm install @scope/private-package-name // 安装私有包
npm install example-package@<tag> // 安装指定版本的包
npm install -g <package_name> // 全局安装
npm unstall
```

## 包更新
```js
npm update // 更新本地包
npm outdated // 查看本地包是否有更新
npm outdated -g --depth=0 // 查看全局要更新的包
npm update -g <package_name> //更新单个包
npm update -g // 更新全局包
```


## NPM 包发布
```js
npm version <update_type> // 更改包版本
npm publish // 发布到npm
```

## NPM 包删除
```js
npm unpublish <package-name> -f //强制删除
npm unpublish <package-name>@<version> //指定版本号
```

## NPM 包登陆
```js
npm login // 登陆
npm logout // 退出
```

## NPM 包用户
```js
npm whoami // 查看是否登陆
npm adduser // 添加用户
```

## NPM 设置
```js
npm set registry [url] (npm conifg set registry [url]) // 查看源
npm get registry [url] (npm conifg get registry [url]) // 更改源
```

## NPM scope

- NPM 支持私有包，但是`--scope=@my-username`的`my-username`必须是账户名称，不然会一直报权限问题
- NPM 支持私有包的发布必须要加上`--access public`，否则会失败

```js
npm init --scope=@my-org // 初始化一个组织性质的scope包
npm init --scope=@my-username // 初始化一个用户性质的scope包
npm publish --access public // 发布一个公开的scope包
npm install @scope/package-name // 安装scope包
```

## NPM 添加权限
```js
npm owner add <user> <your-package-name> // 给私有包添加贡献者权限
```

## 其他

```js
npm cache clean // 清除包缓存
```