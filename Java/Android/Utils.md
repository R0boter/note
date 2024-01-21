## Gradle

Gradle 是一个项目自动化构建工具，用于依赖，打包，部署，发布，各种渠道的差异管理等工作

注意：**每个版本的 Android-Studio 都有对应的 Gradle 版本，只有二者的版本正确对应，App 工程才能成功编译**

[studio 和 gradle 版本对应详情](https://developer.android.google.cn/studio/releases/gradle-plugin#updating-plugin)

## 配置文件

项目级别的 build.gradle 指定了当前项目的总体编译规则，而模块级别的 build.gradle 对应于具体模块，每个模块都有自己的 build.gradle，它指定了当前模块的详细编译规则

## 项目级

```gradle
buildscript {
  // 用于设置插件的网络仓库地址
  repositories {
    // 添加四行阿里云仓库地址，方便国内下载，低版本的 url 后是空格，高版本是等号
    maven { url="https://maven.aliyun.com/repository/jcenter" }
    maven { url="https://maven.aliyun.com/repository/google" }
    maven { url="https://maven.aliyun.com/repository/gradle-plugin" }
    maven { url="https://maven.aliyun.com/repository/public" }
    google()
    jcenter()
  }

  // 用于设置 gradle 插件的版本好
  dependencies {

  }
}

// 项目引入的插件
plugins {
  id 'com.android.application' version '7.1.2' apply false
}

// 全局执行任务，下面是删除之前编译的目录
task clean(type: Delete){
  delete rootProject.buildDir
}
```

## 模块级

```gradle
android {
  // 指定编译时的 SDK 版本号，30 表示 android 11
  compileSdkVersion 30
  // 指定编译工具的版本号，大版本必须和上面保持一致，具体版本号在 SDK 安装目录下的 build-tools 下找到
  buildToolsVersion "30.0.3"
  defaultConfig {
    // 指定该模块的应用编号，也就是 app 包名
    applicationId "com.example.appname"
    // 指定 app 适合运行的最小 SDK 版本号
    minSdkVersion 19
    // 指定目标设备的 SDK 版本号，即 app 希望在哪个版本的 android 上运行
    minSdkVersion 30
    // 指定 app 的应用版本号
    minSdkVersion 1
    // 指定 app 的应用版本名称
    minSdkVersion "1.0"

    // 单元测试
    testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
  }
  buildTypes {
    release {
      minifyEnabled false
      proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
    }
  }
}

// 指定 App 编译的依赖信息
dependencies {
  // 指定引用 jar 包的路径
  implementation fileTree(dir: 'libs', include: ['*.jar'])
  // 指定编译 android 的高版本支持库， 如 AppCompatActivity 必须指定编译 appcompat 库
  implementation 'androidx.appcompat:appcompat:1.2.0'
  // 指定单元测试编译用的 junit 版本号
  testImplementation 'junit:junit:4.13'
  androidTestImplementation 'androidx.test.ext:junit:1.1.2'
  androidTestImplementation 'androidx.test.espresso:espresso-core:3.3.0'
}
```
