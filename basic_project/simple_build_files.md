# Simple build files（簡單的構建文件）

一個最簡單的Gradle純Java項目的build.gradle文件包含以下內容：

    apply plugin: 'java'

這裡引入了Gradle的Java插件。這個插件提供了所有構建和測試Java應用程序所需要的東西。

最簡單的Android項目的build.gradle文件包含以下內容：

    buildscript {
        repositories {
            mavenCentral()
        }

        dependencies {
            classpath 'com.android.tools.build:gradle:0.11.1'
        }
    }

    apply plugin: 'android'

    android {
        compileSdkVersion 19
        buildToolsVersion "19.0.0"
    }

這裡包括了Android build file的3個主要部分：

`buildscrip{...}`這裡配置了驅動構建過程的代碼。

在這個部分，它聲明瞭使用Maven倉庫，並且聲明瞭一個maven文件的依賴路徑。這個文件就是包含了0.11.1版本android gradle插件的庫。

---

> 注意：這裡的配置隻影響控制構建過程的代碼，不影響項目源代碼。項目本身需要聲明自己的倉庫和依賴關係，稍後將會提到這部分。

---

接下來，跟前面提到的Java Plugin一樣添加了`android` plugin。

最後，`andorid{...}`配置了所有android構建過程需要的參數。這裡也是Android DSL的入口點。

默認情況下，只需要配置目標編譯SDK版本和編譯工具版本，即`compileSdkVersion`和`buildToolsVersion`屬性。
這個`complieSdkVersion`屬性相當於舊構建系統中project.properites文件中的`target`屬性。這個新的屬性可以跟舊的`target`屬性一樣指定一個int或者String類型的值。

---

> 重要：你只能添加`android` plugin。同時添加`java` plugin會導致構建錯誤。

---

> 注意：你同樣需要在相同路徑下添加一個local.properties文件，並使用sdk.dir屬性來設置SDK路徑。
另外，你也可以通過設置`ANDROID_HOME`環境變量，這兩種方式沒有什麼不同，根據你自己的喜好選擇其中一種設置。

---
