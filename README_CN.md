[![Serverless Framework Tencent Cloud Plugin](https://s3.amazonaws.com/assets.general.serverless.com/component_website_tencent/readme-website-tencent-serverless.png)](http://serverless.com)

&nbsp;

# 腾讯云静态网站组件

## 简介

静态网站应用调用了基础的腾讯云COS组件，可以快速部署静态网站页面到对象存储COS中，并生成域名供访问。

## 快速开始

操作步骤如下：

1. [安装](#1-安装)
2. [创建](#2-创建)
3. [配置](#3-配置)
4. [部署](#4-部署)
5. [移除](#5-移除)

&nbsp;

### 1. 安装

通过npm安装serverless

```console
$ npm install -g serverless
```

### 2. 创建

本地创建my-website文件夹

```console
$ mkdir my-website
$ cd my-website
```
在文件夹中创建对应的 `serverless.yml` 和 `.env` 两个文件，并将静态页面放在`code`目录下，文件目录结构如下：

```
|- code
  |- index.html
|- serverless.yml
|- .env      # your Tencent SecretId/Key/AppId

```

在 `.env` 文件中配置腾讯云的APPID，SecretId和SecretKey信息并保存

如果没有腾讯云账号，可以在此[注册新账号](https://cloud.tencent.com/register)。

如果已有腾讯云账号，可以在[API密钥管理
](https://console.cloud.tencent.com/cam/capi)中获取`APPID`, `SecretId` 和`SecretKey`.

```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```

* `code`目录下应该对应html/css/js资源的文件，或者一个完整的React应用

示例html[下载地址](https://tinatest-1251971143.cos.ap-beijing.myqcloud.com/index.html)

该例子，也可以将以下代码放入到index.html文件中：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello, Tencent Cloud</title>
</head>
<body>
Hello, Tencent Cloud
</body>
</html>
```

### 3. 配置

在serverless.yml中进行如下配置


```yml
# serverless.yml

myWebsite:
  component: "@tencent-serverless/tencent-website-beta"
  inputs:
    code:
      src: ./code
      index: index.html
      error: index.html
    region: ap-guangzhou
    bucketName: my-bucket

```

* [点击此处查看配置文档](https://github.com/serverless-tencent/tencent-website/blob/master/docs/configure.md)


### 4. 部署

通过如下命令进行部署，并查看部署过程中的信息
```console
$ sls --debug
  
    DEBUG ─ Resolving the template's static variables.
    DEBUG ─ Collecting components from the template.
    DEBUG ─ Downloading any NPM components found in the template.
    DEBUG ─ Analyzing the template's components dependencies.
    DEBUG ─ Creating the template's components graph.
    DEBUG ─ Syncing template state.
    DEBUG ─ Executing the template's components graph.
    DEBUG ─ Starting Website Component.
    DEBUG ─ Preparing website Tencent COS bucket my-bucket-1300415943.
    DEBUG ─ Deploying "my-bucket-1300415943" bucket in the "ap-guangzhou" region.
    DEBUG ─ "my-bucket-1300415943" bucket was successfully deployed to the "ap-guangzhou" region.
    DEBUG ─ Setting ACL for "my-bucket-1300415943" bucket in the "ap-guangzhou" region.
    DEBUG ─ Ensuring no CORS are set for "my-bucket-1300415943" bucket in the "ap-guangzhou" region.
    DEBUG ─ Ensuring no Tags are set for "my-bucket-1300415943" bucket in the "ap-guangzhou" region.
    DEBUG ─ Configuring bucket my-bucket-1300415943 for website hosting.
    DEBUG ─ Uploading website files from /Users/dfounderliu/Desktop/temp/code/src to bucket my-bucket-1300415943.
    DEBUG ─ Starting upload to bucket my-bucket-1300415943 in region ap-guangzhou
    DEBUG ─ Uploading directory /Users/dfounderliu/Desktop/temp/code/src to bucket my-bucket-1300415943
    DEBUG ─ Website deployed successfully to URL: https://my-bucket-1300415943.cos-website.ap-guangzhou.myqcloud.com.
  
    myWebsite: 
      url: https://my-bucket-1300415943.cos-website.ap-guangzhou.myqcloud.com
      env: 
  
    2s › myWebsite › done

```



### 5. 移除

通过以下命令移除项目
```console
sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Starting Website Removal.
  DEBUG ─ Removing Website bucket.
  DEBUG ─ Removing files from the "my-bucket-1300415943" bucket.
  DEBUG ─ Removing "my-bucket-1300415943" bucket from the "ap-guangzhou" region.
  DEBUG ─ "my-bucket-1300415943" bucket was successfully removed from the "ap-guangzhou" region.
  DEBUG ─ Finished Website Removal.

  3s › myWebsite › done
```

### 还支持哪些组件？

可以在 [Serverless Components](https://github.com/serverless/components) repo 中查询更多组件的信息。
