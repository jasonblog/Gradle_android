# Using sourceCompatibility 1.7（使用（JDK）1.7版本的sourceCompatibility）

使用Android KitKat（19版本的buildTools）就可以使用diamond operator，multi-catch，switch中使用字符串，try with resource等等（譯註：都是JDK7的一些新特性，詳情請參考JDK7文檔）。設置使用1.7版本，需要修改你的構建文件：

    android {
        compileSdkVersion 19
        buildToolsVersion "19.0.0"

        defaultConfig {
            minSdkVersion 7
            targetSdkVersion 19
        }

        compileOptions {
            sourceCompatibility JavaVersion.VERSION_1_7
            targetCompatibility JavaVersion.VERSION_1_7
        }
    }

---

> 注意：你可以將`minSdkVersion`的值設置為19之前的版本，只是你只能使用除了try with resources之外的其它新語言特性。如果你想要使用try with resources特性，你就需要把`minSdkVersion`也設置為19。

---

你同樣也需要確認Gradle使用1.7或者更高版本的JDK（Android Gradle plugin也需要0.6.1或者更高的版本）。
