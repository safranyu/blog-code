---
title: 快速搭建Flutter环境-Mac
comments: true
categories:
  - Flutter
tags:
  - Flutter
abbrlink: 9a98d699
date: 2019-09-15 21:37:25
---
## 目录

- 系统要求
- 设置FLutter镜像(非必须)
- 获取Flutter SDK
- iOS开发环境设置
- Android开发环境设置
- 安装Flutter插件

## 系统要求

在Mac上要安装并运行Flutter要满足以下最低要求:

- 操作系统: macOS (64-bit)
- 磁盘空间: 700 MB (不包括Xcode或Android Studio的磁盘空间）.
- 工具: Flutter 依赖下面这些命令行工具：`bash curl git 2.x mkdir rm unzip which`

## 设置FLutter镜像(非必须)

由于在国内访问Flutter可能会受到限制，Flutter官方为中国开发者搭建了临时镜像，大家可以将如下环境变量加入到用户环境变量中：

```javascript
//Macintosh HD⁩ ▸ ⁨Users⁩ ▸ ⁨你的用户名 ▸ ⁨.bash_profile
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn

```

注意：此镜像为临时镜像，并不能保证一直可用，大家可以从 [Using Flutter in China](https://flutter.dev/community/china) 上获得有关镜像服务器的最新动态。

## 获取Flutter SDK

**1.点Flutter官网下载其最新可用的安装包。**

**2.解压安装包到你想安装的目录，如：**

```shell
$ cd ~/development
$ unzip ~/Downloads/flutter_macos_v1.2.1-stable.zip
```

**3.添加flutter相关工具到path中：**

```javascript
 export PATH="$PATH:`pwd`/flutter/bin"
```

此代码只能暂时针对当前命令行窗口设置PATH环境变量，要想永久将Flutter添加到PATH中请参考下面做法：

```shell
$ cd ~
$ vim .bash_profile
```

然后添加：

```javascript
export PATH=/Users/safran/Documents/flutter/bin:$PATH
```

之后记得保存文件。

### 运行 flutter doctor

上面path配置完成之后，需要关闭终端重新打开，然后运行：

```shell
$ flutter doctor
```

该命令检查你的环境并在终端窗口中显示报告。Dart SDK已经在捆绑在Flutter里了，没有必要单独安装Dart。 仔细检查命令行输出以获取可能需要安装的其他软件或进一步需要执行的任务（以粗体显示）：

例如：

```
[-] Android toolchain - develop for Android devices
    • Android SDK at /Users/obiwan/Library/Android/sdk
    ✗ Android SDK is missing command line tools; download from https://goo.gl/XxQghQ
    • Try re-installing or updating your Android SDK,
      visit https://flutter.dev/setup/#android-setup for detailed instructions.
```

一般的错误会是XCode或Android Studio版本太低、或者没有`ANDROID_HOME`环境变量等，可参考一下环境变量的配置来检查你的环境变量：

```shell
#flutter环境变量
export PATH=/Users/safran/Desktop/flutter/bin:$PATH
# flutter镜像
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
#Android 环境变量
export ANDROID_HOME=/Users/safran/Library/Android/sdk
#Android 模拟器路径
export PATH=${PATH}:${ANDROID_HOME}/emulator
#Android tools路径
export PATH=${PATH}:${ANDROID_HOME}/tools
#Android 平台工具路径
export PATH=${PATH}:${ANDROID_HOME}/platform-tools
#Android NDK路径
ANDROID_NDK_HOME=/Users/safran/Library/Android/ndk/android-ndk-r10e
```

> *第一次运行一个flutter命令（如flutter doctor）时，它会下载它自己的依赖项并自行编译。以后再运行就会快得多。*

## iOS开发环境设置

### 安装 Xcode

要用Flutter开发iOS App需要Xcode 9.0 或更高版本:

**1.安装Xcode 9.0或更新版本(通过链接下载或苹果应用商店)**

**2.配置Xcode命令行工具以使用新安装的Xcode版本**

```shell
$ sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```

以上路径时对于最新版Xcode的路径。如果你需要使用不同的Xcode版本，需要指定相应路径。

**3.确保Xcode许可协议是通过打开一次Xcode或通过命令sudo xcodebuild -license同意过了**

接下来就可以使用Xcode，在iOS设备或模拟器上运行Flutter App了。

### 设置iOS模拟器

要准备在iOS模拟器上运行并测试您的Flutter应用，请按以下步骤操作：

**1.在终端输入如下命令打开一个iOS模拟器：**

```shell
$ open -a Simulator
```

**2.通过模拟器菜单栏的 硬件>设备 ，确保你打开是64位 iPhone 5s或更新的模拟器**

**3.如果模拟器过大，可以通过模拟器的 Window> Scale 菜单下设置设备比例**

### 创建和运行一个简单的Flutter项目

**1.通过如下命令创建一个Flutter项目**

```shell
$ flutter create my_app
```

**2.命令运行完成之后会在当前目录下创建一个名为my_app的Flutter项目，然后通过一下命令可以运行它：**

```shell
$ cd my_app
$ flutter run
```

### 如何将Flutter安装到iOS真机上？

要通过`lutter run`将Flutter应用安装到iOS真机设备，需要一些额外的工具和一个Apple帐户，还需要在Xcode中进行设置：

> 当然，用XCode来将Flutter运行在真机上更简单，只需要点一下`run`按钮即可，可以根据需要进行选择这两种不同的运行方式；

**1.安装 Homebrew （如果已经安装了brew,跳过此步骤）.**

**2.确保homebrew已更新**

```shell
$ brew update
```

**3.打开终端并运行这些命令来安装用于将Flutter应用安装到iOS设备的工具**

```shell
$ brew install --HEAD usbmuxd
$ brew link usbmuxd
$ brew install --HEAD libimobiledevice
$ brew install ideviceinstaller ios-deploy cocoapods
$ pod setup
```

如果这些命令中的任何一个失败并出现错误，可运行`brew doctor`并按照说明解决问题。

**4.遵循Xcode签名流程来配置您的项目:**

- 在你Flutter项目目录中通过 `open ios/Runner.xcworkspace` 打开默认的Xcode workspace
- 在Xcode中，选择导航面板左侧中的Runner项目
- 在Runner target设置页面中，确保在 常规>签名>团队 下选择了您的开发团队。当您选择一个团队时，Xcode会创建并下载开发证书，向您的设备注册您的帐户，并创建和下载配置文件（如果需要）
  - 要开始您的第一个iOS开发项目，您可能需要使用您的Apple ID登录Xcode



- 任何Apple ID都支持开发和测试，但如果要将应用发布到App Store则需要一个99美刀的开发者账号。
- 当你第一次attach真机设备进行iOS开发时，需要同时信任你的Mac和该设备上的开发证书。首次将iOS设备连接到Mac时,请在对话框中选择 `Trust`。

然后，转到iOS设备上的设置应用程序，选择 常规>设备管理 并信任您的证书。

- 如果Xcode中的自动签名失败，请验证项目的 General > Identity > Bundle Identifier 值是否唯一。

**5.通过flutter run运行启动项目**

```shell
$ flutter run
```

## Android开发环境设置&Flutter插件安装

### 安装Android Studio

**1.下载并安装 Android Studio**

- https://developer.android.com/studio
- https://developer.android.google.cn/studio

> 因为Android网站设在国外，如果你的网络无法访问第一个地址，可以选择使用Google为中国开发者提供的中国网址进行访问。

另外，关于Android Studio的安装和配置，Android官方有比较详细的说明文档https://developer.android.google.cn/studio/intro，大家可以根据需要进行查阅；

**2.启动Android Studio，然后执行“Android Studio安装向导”。这将安装最新的Android SDK，Android SDK平台工具和Android SDK构建工具**

### Flutter插件安装

- 打开Android Studio
- 打开Preferences > Plugins (macOS), File > Settings > Plugins (Windows & Linux)
- 选择 Browse repositories, 搜索 Flutter plugin
- 然后点击安装，然后安装Dart插件
- 完成之后选择重启Android Studio

### 如何在Android模拟器上运行Flutter？

要准备在Android模拟器上运行并测试您的Flutter应用，需要按照以下步骤操作：

- 在你的机器上启用 [VM acceleration](https://developer.android.com/studio/run/emulator-acceleration.html#vm-mac)；

- 启动 Android Studio>Tools>Android>AVD Manager 并选择 `Create Virtual Device`；

- 选择一个设备并选择 Next；

- 为要模拟的Android版本选择一个或多个系统映像，然后选择 Next. 建议使用 x86 或 x86_64 的镜像；

- 在 Emulated Performance下, 选择 Hardware - GLES 2.0 以启用硬件加速；

- 验证AVD配置是否正确，然后选择 Finish；

  如果对以上步骤还有不清楚的可以参阅Android官方的 [Managing AVDs](https://developer.android.com/studio/run/managing-avds.html)文档。

- 在 Android Virtual Device Manager中, 点击工具栏的 `Run`，模拟器启动并显示所选操作系统版本或设备的启动画面；

- 通过`flutter run`运行启动项目；

### 如何在Android真机运行？

要准备在Android设备上运行并测试您的Flutter应用，您需要安装Android 4.1（API level 16）或更高版本的Android设备

- 在你的设备上启用 `开发人员选项` 和 `USB调试` 。详细说明可在[Android文档](https://developer.android.com/studio/debug/dev-options.html)中找到；
- 使用USB将手机插入电脑，如果有授权提示需要同意授权；
- 在终端中，运行` flutter devices` 命令以验证Flutter是否识别你连接的Android设备；
- 通过`flutter run`运行启动项目；

默认情况下，Flutter使用的Android SDK版本是基于你的 `adb` 工具版本， 如果你想让Flutter使用不同版本的Android SDK，则必须将该 `ANDROID_HOME` 环境变量修改SDK的目录。

## 参考

- [两分钟带你快速搭建Flutter开发环境(Mac)](http://www.devio.org/2019/04/03/development-environment-mac/)