---
title: Android studio中用gradle统一版本。
tags:
  - Android studio
  - gradle
categories:
  - Android studio
date: 2018-5-03 15:30:22
---

如果我们的项目比较小，只有一个moudle，那么我们在导入第三方库，或者设置minSdkVersion，targetSdkVersion等参数时，直接在moudle的build.gradle的相关位置进行设置就可以了，如果我们的项目比较庞大，有很多个moudle，特别是当我们使用组件化开发时，有多个gradle文件需要导入相同的配置，这时候如果按照老方法在build.gradle中写死我们的配置的话，是非常不方便修改的。这时候，我们就需要将gradle中的参数抽取出来，放到另外一个文件中，然后再在每个build.gradle文件中进行引入即可。
<!-- more -->

### 创建配置文件config.gradle

```bash
ext {

    android = [
            targetSdkVersion : 27,
            compileSdkVersion: 27,
            buildToolsVersion: '25.0.2',
            minSdkVersion    : 21,
            versionCode      : 1,
            versionName      : "1.0",
    ]
    dependVersion = [
            support: '27.1.1'
    ]
    gradle = [
            gradle_version: "3.1.3"
    ]
    kotlin = [
            kotlin_version: '1.2.31',
    ]
    dependencies = [
            // ------------- Android -------------
            supportV4            : "com.android.support:support-v4:${dependVersion.support}",
            appcompatV7          : "com.android.support:appcompat-v7:${dependVersion.support}",
            design               : "com.android.support:design:${dependVersion.support}",
            constraintLayout     : 'com.android.support.constraint:constraint-layout:1.1.2',
            //------------- 测试 -------------
            junit                : 'junit:junit:4.12',
            testRunner           : 'com.android.support.test:runner:1.0.2',
            espresso             : 'com.android.support.test.espresso:espresso-core:3.0.2',
            // ------------- 网络请求 -------------
            okhttp               : 'com.squareup.okhttp3:okhttp:3.3.1',
            retrofit             : 'com.squareup.retrofit2:retrofit:2.1.0',

            // ------------- 图片加载 -------------
            fresco               : 'com.facebook.fresco:fresco:0.11.0',
            animatedGif          : 'com.facebook.fresco:animated-gif:0.12.0',
            picasso              : 'com.squareup.picasso:picasso:2.5.2',
            photoView            : 'com.github.chrisbanes:PhotoView:1.3.1',

            // ------------- RxAndroid -------------
            rxAndroid            : 'io.reactivex:rxandroid:1.2.1',
            rxJava               : 'io.reactivex:rxjava:1.2.2',

            // ------------- json解析 -------------
            fastJson             : 'com.alibaba:fastjson:1.1.54.android',
            gson                 : 'com.google.code.gson:gson:2.8.0',

            // ------------- log打印工具 -------------
            logger               : 'com.orhanobut:logger:1.15',

            greendao             : 'org.greenrobot:greendao:3.2.0',

            // ------------- ButterKnife -------------
            butterknife          : 'com.jakewharton:butterknife:8.4.0',
            butterknifeCompiler  : 'com.jakewharton:butterknife-compiler:8.4.0',

            // ------------- LeakCanary -------------
            leakcanaryAndroid    : 'com.squareup.leakcanary:leakcanary-android:1.5',
            leakcanaryAndroidNoOp: 'com.squareup.leakcanary:leakcanary-android-no-op:1.5',
            // ------------- activityrouter -------------
            activityrouter       : 'com.github.mzule.activityrouter:activityrouter:1.2.2',
    ]

}
```

### 项目Project中的build.gradle对该配置文件进行引入
```bash
buildscript {
    apply from: "config.gradle"
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath "com.android.tools.build:gradle:$rootProject.ext.gradle.gradle_version"
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$rootProject.ext.kotlin.kotlin_version"
    }
}

allprojects {
    repositories {
        google()
        jcenter()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
```

### moudle中的build.gradle的配置方式
```bash
apply plugin: 'com.android.application'

apply plugin: 'kotlin-android'

apply plugin: 'kotlin-android-extensions'

android {
    compileSdkVersion rootProject.android.compileSdkVersion
    defaultConfig {
        applicationId "lieeber.com.androidcomponent"
        minSdkVersion rootProject.android.minSdkVersion
        targetSdkVersion rootProject.android.targetSdkVersion
        versionCode rootProject.android.versionCode
        versionName rootProject.android.versionName
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    implementation fileTree(include: ['*.jar'], dir: 'libs')
    implementation project(':common')
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jre7:$rootProject.ext.kotlin.kotlin_version"
    implementation rootProject.ext.dependencies.appcompatV7
    implementation rootProject.ext.dependencies.constraintLayout
    testImplementation rootProject.ext.dependencies.junit
    androidTestImplementation rootProject.ext.dependencies.testRunner
    androidTestImplementation rootProject.ext.dependencies.espresso
}
```

可以看出，配置文件是很灵活的，我们可以按照自己的习惯或者项目的情况来进行分组，不同的moudle都可以进行引入，当需要修改版本号或者对第三方库进行升级时，只需要在config.gradle修改就可以了。


