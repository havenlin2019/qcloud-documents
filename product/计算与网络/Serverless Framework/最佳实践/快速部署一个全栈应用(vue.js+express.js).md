## 操作场景
全栈组件（Vue.js+Express.js）用于通过多个 Serverless Components 部署 Serverless 全栈应用程序。可以帮助开发者更方便快捷的部署 Serverless 应用，例如利用后端 API 与前端 Vue.js 结合等场景。

此项目完全基于腾讯云 Serverless 服务器，可很大程度的缩减使用成本。 如果您正在寻找一个低开销的便捷轻量的 Serverless 服务管理框架，全栈组件（Vue.js+Express.js）将是很好的选择。

该 Template 包括：
* **serverless Express.js 后端**：由腾讯云 Servelress Cloud Function（云函数 SCF） 和腾讯云 API 网关提供相关能力，支持 express.js 框架，帮助开发者架构自己的项目和路由。
* **serverless Vue.js 前端**：由腾讯云 Cloud Object Storage（对象存储 COS）提供相关存储能力，通过后端 API 传递到前端，并使用 Vue.js 做相关渲染。

该全栈 Web 应用架构图如下：
![架构图](https://main.qcloudimg.com/raw/21ae7465b6927c14d9bc4ae6dc33fc17.png)

## 操作步骤
#### 安装

1. 通过如下命令安装 [Serverless Framework](https://www.github.com/serverless/serverless)：
```console
$ npm i -g serverless
```
2. 新建一个本地文件夹，使用 `create --template-url` ，安装相关 template。您也可以将文件直接下载到本地：
```console
$ serverless create --template-url https://github.com/serverless/components/tree/master/templates/tencent-fullstack-application
```
使用`cd`命令，进入`templates\tencent-fullstack-application` 文件夹，可以查看到如下目录结构：
```
|- api
|- dashboard
|- serverless.yml      # 使用项目中的 yml 文件
```
分别在`dashboard` 和 `api` 两个文件目录执行 NPM 依赖的安装，如下命令所示：
```console
$ cd dashboard
$ npm i
```
```
$ cd api
$ npm i
```

#### 部署

回到`tencent-fullstack-application`目录下，直接通过 `serverless` 命令来部署应用:

```console
$ serverless
```

如果希望查看部署详情，可以通过调试模式的命令 `serverless --debug` 进行部署。

如您的账号未 [登录](https://cloud.tencent.com/login) 或 [注册](https://cloud.tencent.com/register) 腾讯云，您可以直接通过微信扫描命令行中的二维码进行授权登录和注册。

部署成功后，可以直接在浏览器中访问日志中返回的 dashboard url 地址，查看该全栈 Web App 的效果：
```
  dashboard:
    url: https://jcwm1l-myappid.cos-website.ap-guangzhou.myqcloud.com
    env:
      apiUrl: https://service-id-myappid.gz.apigw.tencentcs.com/release/
  api:
    region:              undefined
    functionName:        tencent-fullstack-api
    apiGatewayServiceId: service-id
    url:                 https://service-id-myappid.gz.apigw.tencentcs.com/release/

  15s » dashboard » done
```

&nbsp;

#### 注意事项
1. 首次部署成功后，也可以通过以下命令，在本地运行服务，并与后端腾讯云服务进行通讯：
```console
$ cd dashboard && npm run start
```

2. 目前暂不支持淘宝等第三方 npm 源，如报错`Component "@serverless/tencent-express" was not found on NPM nor could it be resolved locally.`请设置并使用 npm 官方源体验：
```console
$ npm config rm registry
$ npm set registry https://registry.npmjs.org/
```

3. 腾讯云 Component 已支持二维码一键登录，如您希望使用配置密钥的方式登录，也可以参考如下步骤：
在`tencent-fullstack-application` 文件夹根目录创建 `.env` 文件：
```console
$ touch .env # 腾讯云的配置信息
```
在 `.env` 文件中配置腾讯云的 SecretId 和 SecretKey 信息并保存
如果没有腾讯云账号，请先 [注册新账号](https://cloud.tencent.com/register)。
如果已有腾讯云账号，可以在 [API 密钥管理](https://console.cloud.tencent.com/cam/capi) 中获取 SecretId 和 SecretKey。
```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```

