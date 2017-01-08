# Creating a Library Project（創建一個庫項目）

一個庫項目與通常的Android項目非常類似，只是有一點小區別。

儘管構建庫項目不同於構建應用程序，它們使用了不同的plugin。但是在內部這些plugin共享了大部分相同的代碼，並且它們都由相同的com.android.tools.build.gradle.jar提供。

    buildscript {

        repositories {
            mavenCentral()
        }


        dependencies {
            classpath 'com.android.tools.build:gradle:0.5.6'
        }

    }

    apply plugin: 'android-library'

    android {
        compileSdkVersion 15
    }

這裡創建了一個使用API 15編譯_SourceSet_的庫項目，並且依賴關係的配置方法與應用程序項目的配置方法一樣，同樣也支持自定義配置。
