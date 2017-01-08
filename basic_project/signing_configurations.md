# signing configurations（簽名配置）

對一個應用程序簽名需要以下：

* 一個Keystory
* 一個keystory密碼
* 一個key的別名
* 一個key的密碼
* 存儲類型

位置，鍵名，兩個密碼，還有存儲類型一起形成了簽名配置。

默認情況下，`debug`被配置成使用一個debug keystory。
debug keystory使用了默認的密碼和默認key及默認的key密碼。
debug keystory的位置在$HOME/.android/debug.keystroe，如果對應位置不存在這個文件將會自動創建一個。

`debug` _Build Type_(構建類型) 會自動使用`debug` _SigningConfig_ (簽名配置)。

可以創建其他配置或者自定義內建的默認配置。通過`signingConfigs`這個DSL容器來配置：

    android {
        signingConfigs {
            debug {
                storeFile file("debug.keystore")
            }

            myConfig {
                storeFile file("other.keystore")
                storePassword "android"
                keyAlias "androiddebugkey"
                keyPassword "android"
            }
        }

        buildTypes {
            foo {
                debuggable true
                jniDebugBuild true
                signingConfig signingConfigs.myConfig
            }
        }
    }

以上代碼片段修改debug keystory的路徑到項目的根目錄下。在這個例子中，這將自動影響其他使用到`debug`構建類型的構建類型。

這裡也創建了一個新的`Single Config`（簽名配置）和一個使用這個新簽名配置的新的`Build Type`（構建類型）。

---
> 注意：只有默認路徑下的debug keystory不存在時會被自動創建。更改debug keystory的路徑並不會自動在新路徑下創建debug keystory。如果創建一個新的不同名字的_SignConfig_，但是使用默認的debug keystore路徑來創建一個非默認的名字的SigningConing，那麼還是會在默認路徑下創建debug keystory。換句話說，會不會自動創建是根據keystory的路徑來判斷，而不是配置的名稱。

---

> 注意：雖然經常使用項目根目錄的相對路徑作為keystore的路徑，但是也可以使用絕對路徑，儘管這並不推薦（除了自動創建出來的debug keystore）。

---

> __注意：如果你將這些文件添加到版本控制工具中，你可能不希望將密碼直接寫到這些文件中。下面Stack Overflow鏈接提供從控制檯或者環境變量中獲取密碼的方法：
http://stackoverflow.com/questions/18328730/how-to-create-a-release-signed-apk-file-using-gradle
我們以後還會在這個指南中添加更多的詳細信息。__

---
