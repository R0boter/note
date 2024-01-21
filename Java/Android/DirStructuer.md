## App 工程目录结构

App 工程分为两个层次，第一个层次是项目，另一个层次是模块。模块依附于项目，每个项目至少有一个模块，也可以有多个模块。

一般所言的“编译运行App”，是指运行某个模块，而非某个项目，因为模块才对应实际的 App

一个 App 在 android-studio android 视图下一般呈现两个分类，一个是 app（代表 app 模块），一个是 Gradle Scripts（工程编译配置文件）

## app 模块

- manifests 子目录，下面只有一个 xml 文件，即 AndroidManifest.xml，它是 App 的运行配置文件
- java 子目录，下面有 3 个 com.example.myapp 包，其中第一个存放当前模块的 java 源代码，后面两个存放测试用的 java 代码
- res 子目录，存放当前模块的资源文件，下面又有 4 个子目录
  - drawable 目录，存放图形描述文件与图片文件
  - layout 目录，存放 App 页面的布局文件
  - mipmap 目录，存放 App 启动图标
  - values 目录，存放一些常量定义文件
    - 字符串常量，strings.xml
    - 像素常量，dimens.xml
    - 颜色常量，colors.xml
    - 样式风格定义，styles.xml

### 清单文件

AndroidManifest.xml 指定了 App 的运行配置信息，是一个 XML 描述文件

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- package 属性指定了该 App 的包名 -->
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.example.appname">
  <application
    <!-- 是否允许应用备份，允许用户备份系统应用和第三方引用的 apk 安装包和应用数据 -->
    android:allowBackup="true"
    <!-- 指定 App 在手机屏幕上显示的图标 -->
    android:icon="@mipmap/ic_launcher"
    <!-- 指定 App 在手机屏幕上显示的名称 -->
    android:label="app_name"
    <!-- 指定 App 的圆角图标 -->
    android:roundIcon="@mipmap/ic_launcher_round"
    <!-- 是否支持阿拉伯语/波斯语这种从右往左的文字排列顺序 -->
    android:supportsRtl="true"
    <!-- 指定 App 的主题 -->
    android:theme="@style/AppTheme"
  >

  <!-- 活动页面的注册声明，只有在此文件中正确配置了 activity 节点，才能在运行时访问对应的活动页面 -->
  <!-- 初始配置的 MainActivity 正是 App 的默认主页 -->
  <activity android:name=".MainActivity">
    <!-- 过滤规则 -->
    <intent-filter>
      <!-- action 节点设置的android.intent.action.MAIN 表示该页面是 App 的入口页面 -->
      <action android:name="android.intent.action.MAIN"/>
      <!-- category 节点设置的android.intent.category.LAUNCHER 决定了是否在手机屏幕上显示 App 图标 -->
      <!-- 如果有两个 activity 节点中都设置了，那么桌面会显示两个 App 图标 -->
      <category android:name="android.intent.category.LAUNCHER"/>
    </intent-filter>
  </activity>

  </application>
</manifest>
```

## Gradle Scripts

- build.gradle，该文件分为项目级和模块级两种，用于描述 App 工程的编译规则
- proguard-rules.pro，该文件用于描述 java 代码的混淆规则
- gradle.properties，该文件用于配置编译工程的命令行参数，一般无需改动
- settings.gradle，该文件用于配置需要编译哪些模块，初始内容为 `include':app'`，表示只编译 app 模块
- local.properties，该项目的本地配置文件，它在工程编译时自动生成，用于描述开发者电脑的配置环境，包括 SDK 的本地路径，NDK 的本地路径
