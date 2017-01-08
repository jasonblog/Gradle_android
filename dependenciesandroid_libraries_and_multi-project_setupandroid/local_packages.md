# Local packages（本地包）

配置一個外部庫的jar包依賴，你需要在`compile`配置中添加一個依賴。

    dependencies {
        compile files('libs/foo.jar')
    }

    android {
        ...
    }

---

> 注意：這個`dependencies` DSL標籤是標準Gradle API中的一部分，所以它不屬於`android`標籤。

---

這個`compile`配置將被用於編譯main application。它裡面的所有東西都被會被添加到編譯的classpath中，__同時__也會被打包進最終的APK。
以下是添加依賴時可能用到的其它一些配置選項：

* `compile`
main application（主module）。
* `androidTestCompile`
test application（測試module）。
* `debugCompile`
debug Build Type（debug類型的編譯）。
* `releaseCompile`
release Build Type（發佈類型的編譯）。

因為沒有可能去構建一個沒有關聯任何_Build Type_（構建類型）的APK，APK默認配置了兩個或兩個以上的編譯配置：`compile`和< buildtype >Compile.
創建一個新的_Build Type_將會自動創建一個基於它名字的新配置。

這對於debug版本需要使用一個自定義庫（為了反饋實例化的崩潰信息等）但發佈版本不需要，或者它們依賴於同一個庫的不同版本時會非常有用。
