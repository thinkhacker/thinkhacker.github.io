---
layout: post
title: "iOS最新应用上架App Store流程"
category: 
- iOS
- 应用上架

tags: ["苹果应用上架","iOS应用上架流程","App Store"]
---

* content
{:toc}


<!-- more -->
<!-- TOC -->


# **iOS应用发布流程简要说明**

**简介**：iOS应用上线发布流程一般包含四个部分，第一步是相关证书文件的配置；第二步是Xcode的设置；第三步是iTunes填写App的相关信息；最后是审核结果以及相关邮件回复。

# (一) 开发者发布证书、AppID和描述文件的配置

## 1. 登录Apple开发者中心网站（[苹果开发者中心 https://developer.apple.com](https://developer.apple.com)）

用浏览器输入苹果开发者中心网址，点击右上角Acount，在登录界面上输入用户名和密码进行验证，验证通过后则进入苹果开发者中心。开发者中心主页跟登录界面如下图：




![](![](/media/images/appstore-db5f45ed0036a36b.png)




验证通过后苹果开发者中心，如下图：




![](![](/media/images/appstore-be0d5777468b0541.png)




## 2. 创建Production开发者证书

开发者证书（分为开发和发布两种，类型为iOS Development, iOS Distribution），要上架App Store需要的是iOS Distribution。进入证书创建界面后，点击Certificates，选择All，选择创建（注意：如果已经存在Production证书，从创建发布证书的电脑上面导出P12即可，无需重复创建。）




![](![](/media/images/appstore-5cb6ae418de7d46c.png)




点击右上角小➕号创建发布证书，然后点击页面最下面的Continue按钮，如下图




![](![](/media/images/appstore-ffc33c9ba632f290.png)




在点击最下面的继续后，我们要上传CSR文件，CSR是Certificate Signing Request的英文缩写，即证书请求文件。我们需要在电脑上《钥匙串访问》中生成。




![](![](/media/images/appstore-72f0a0f2a3df0eb4.png)




在选择导入CSR文件后，点击继续以后，然后点击存储，双击下载后的证书就能完成配置。




![](![](/media/images/appstore-9970d6b5b899da90.png)




## 3. 注册App ID

App ID在苹果官方的开发者计划（Apple Developer Member Center）层面，App ID即 Product ID，用于标识一个或者一组App。

首先在证书界面选择App IDs选项，点击右上角➕，可以进入App ID创建界面，如下图：




![](![](/media/images/appstore-6d790aa470d3f7aa.png)







![](![](/media/images/appstore-69fc6708eb4957e4.png)




填完上面的信息过后，继续填写下面的信息，选择注册的功能，选择完成过后点击最下面的Continue按钮，进入最后的页面，点击Register即可完成注册。




![](![](/media/images/appstore-c41321986f832cca.png)






![](![](/media/images/appstore-1fd210fce6721345.png)




## 4. 创建iOS Provisoning Profiles 描述文件

创建完Production发布证书和注册App ID过后，接下来就是创建iOS Provisoning Profiles 描述文件。Provisioning Profile 文件包含了上述的所有内容：证书、App ID 和 设备 ID。




![](![](/media/images/appstore-072ea81975a6f112.png)




点击右上角➕按钮进入iOS Provisoning Profiles 描述文件的创建，创建发布Distribution Provisoning Profiles 需要选择App Store选项。如下图：




![](![](/media/images/appstore-0947fb5e83539b5a.png)




点击继续过后需要你选择上面我们刚创建好的App ID，我们选择对应的App ID即可：




![](![](/media/images/appstore-021684571d3db62a.png)




接着需要我们选择发布者证书，我们选择前面我们创建好的发布证书即可，如下图：




![](![](/media/images/appstore-8969d111822e9d43.png)




点击继续按钮过后，填写Profiles Name后点击继续，然后下载下来，双击安装到电脑即可，如下图：




![](![](/media/images/appstore-81e174d4889d6de4.png)






![](![](/media/images/appstore-cdd9ba0d448d0c52.png)




# (二) Xcode设置

## 1. Xcode工程的应用证书注册

选择工程→TARGETS→General→Signing。如果是Automatically manage signing，将左边的按钮取消掉。然后选择注册我们的Provisoning Profiles 描述文件。




![](![](/media/images/appstore-c95421a93afbba78.png)




## 2. 打包应用APP

工程配置完成后就可以打包APP了，由于是要应用发布，所以需要将工程改成release 模式。

打包APP有几种方式，下面介绍的是平常最常用的打包方式。点击工程，工具栏-Product-Archive，如下图。




![](![](/media/images/appstore-a81a87809e008174.png)




Archive成功后就可以点击 export按钮到处APP包（这里还不能点击Upload App Store，因为itunes connect 上面还没有本应用的项目，需要创建后才能上传）




![](![](/media/images/appstore-5560176723f6ce3e.png)




# (三) iTunes填写App的相关信息

## 1. 登录iTunes Connect




![](![](/media/images/appstore-4c30c6d0711e04e7.png)




## 2. 新App的创建

点击iTunes Connect进入管理界面，如下图。




![](![](/media/images/appstore-63dff4bcc587eea2.png)




点击我的App可以进入App管理界面，在右上角点击➕新建App 即可创建新的App，如下图：




![](![](/media/images/appstore-ef167c684bb7ee57.png)




## 3. App基本信息填写

新建完App后，需要填写App的基本信息，比如App的名称，语言、类别等，详情请参照下图：




![](![](/media/images/appstore-44ba44472dad745d.png)




## 4. App价格与销售范围填写。

填写完App的基本信息后，接着就是填写App的价格及销售范围。一般情况下，App的销售价格为免费的，销售的地区选择所有国家和地区，如果App应用支持bitcode，侧选择自动编译bitcode。如下图：




![](![](/media/images/appstore-a903ddb8fec09adf.png)




## 5. App版本信息填写

填写完成价格与销售范围后，点击左侧xx.x准备提交按钮，即可进入App版本信息填写界面，

首先是添加App预览图和屏幕快照，可直接将对应的图片拖到该区域，如下图：




![](![](/media/images/appstore-6b59a78d78f3d549.png)




App预览图的尺寸大小，如下图所示：




![](![](/media/images/appstore-059a85555021d6b5.png)






![](![](/media/images/appstore-1eba829f7c0b38aa.png)




接着是App的宣传文本，描述以及关键词，分别是需要填写，详情请参照下图：




![](![](/media/images/appstore-6ee754a5ee03b673.png)




填完App的宣传文本关键词后，接下来需要选择上传的App包，即将上面打包好的App包（ipa）通过Application Loader进行上传，上传成功后，构建版本右侧即可出现➕，如下图所示，点击选择对应的版本包即可，




![](![](/media/images/appstore-191085c9e922e1e5.png)




接着填写App的综合信息，如App Store图标，版本，版权等，详情如下图：




![](![](/media/images/appstore-a1e6562fb658915e.png)




最后是填写App的审核信息，包括用户登录名密码，联系人信息等，如下图。填完过后就可以点击右上角保存按钮，提交审核了。




![](![](/media/images/appstore-2f07aa897164b902.png)




# (四) 常见被拒原因以及邮件回复

## 1. 常见被拒原因一

描述：审核过程中，审核人员往往需要更多的信息，如果被拒邮件的描述内容如下

We have started the review of your app, but we are not able to continue because we need additional information about your app.

** Next Steps**

To help us proceed with the review of your app, please review the following questions and provide as much detailed information as you can.

Questions:

1.  Is this app only for your company’s internal use?
2.  If No, which company is your app made for? Please specify the target user’s name.
3.  Can multiple organization or the general public also use your app?
4.  How do users obtain an account? Is it free to get an account?
5.  Is the target audience in China only?

    Once you reply to this message in Resolution Center with the requested information, we can proceed with your review.

解决：根据邮件信息结合我们公司产品特性，我们可以针对性回复以下问题即可。

## 2. 常见被拒原因二

描述，如果苹果回复被拒的邮件是一下内容，并且带有附件图片，如下左图：

Guideline 2.2 - Performance - Beta Testing

Your app includes content or features that users aren't able to use in this version. Apps that are for demonstration, trial, or up-sell purposes are not appropriate for the App Store.

Please see attached screenshots for details.

Next Steps

To resolve this issue, please complete, remove, or fully configure any partially implemented features. Additionally, remove all references to "demo," "trial," "beta," or "test" in your app description, app icon, screenshots, previews, release notes, and binary.

Resources

If you would like to conduct a beta trial for your app, you may wish to review the TestFlight Beta Testing Guide.

解决：一般情况下，这个是苹果审核人员认为是App没有全部开发完成，是测试版本。遇到这个问题，我们只要提供界面数据个测试人员进行测试，如果刚开始没有数据的话，可以回复他们教他们如果操作才能够产生数据。根据信息结合应用我们可以提供App引导。
