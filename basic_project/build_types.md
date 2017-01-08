# Build Types（構建類型）

默認情況下，Android Plugin會自動給項目設置同時構建應用程序的debug和release版本。
兩個版本之間的不同主要圍繞著能否在一個安全設備上調試，以及APK如何簽名。

Debug版本採用使用通用的name/password鍵值對自動創建的數字證書進行簽名，以防止構建過程中出現請求信息。Release版本在構建過程中沒有簽名，需要稍後再簽名。

這些配置通過一個`BuildType`對象來配置。默認情況下，這兩個實例都會被創建，分別是一個`debug`版本和一個`release`版本。

Android plugin允許像創建其他構建類型一樣定製`debug`和`release`實例。這需要在`buildTypes`的DSL容器中配置：

    android {
        buildTypes {
            debug {
                applicationIdSuffix ".debug"
            }

            jnidebug.initWith(buildTypes.debug)
            jnidebug {
                packageNameSuffix ".jnidebug"
                jnidebugBuild true
            }
        }
    }

以上代碼片段實現了以下功能：

* 配置默認的`debug`構建類型
    * 將debug版本的包名設置為<app package>.debug以便能夠同時在一臺設備上安裝_debug_和_release_版本的apk。
* 創建了一個名為`jnidebug`的新構建類型，並且這個構建類型是`debug`構建類型的一個副本。
* 繼續配置`jnidebug`構建類型，允許使用JNI組件，並且也添加了不一樣的包名後綴。

創建一個新的構建類型就是簡單的在`buildType`標籤下添加一個新的元素，並且可以使用`initWith()`或者直接使用閉包來配置它。

以下是一些可能使用到的屬性和默認值：

 Property name	 |Default values for debug	 |Default values for release / other
 ------------- |:-------------:| -----:
 `debuggable`	 |true	 |false
 `jniDebugBuild`	 |false	 |false
 `renderscriptDebugBuild`	 |false	 |false
 `renderscriptOptimLevel`	 |3	 |3
 `applicationIdSuffix`	 |null	 |null
 `versionNameSuffix`	 |null	 |null
 `signingConfig`	 |android.signingConfigs.debug	 |null
 `zipAlign`	 |false	 |true
 `runProguard`	 |false	 |false
 `proguardFile`	 |N/A (set only)	 |N/A (set only)
 `proguardFiles`	 |N/A (set only)	 |N/A (set only)

除了以上屬性之外，_Build Type_還會受項目源碼和資源影響：
對於每一個Build Type都會自動創建一個匹配的_sourceSet_。默認的路徑為：

    src/<buildtypename>/

這意味著_BuildType_名稱不能是_main_或者_androidTest_（因為這兩個是由plugin強制實現的），並且他們互相之間都必須是唯一的。

跟其他sourceSet設置一樣，Build Type的source set路徑可以重新被定向：

    android {
        sourceSets.jnidebug.setRoot('foo/jnidebug')
    }

另外，每一個_Build Type_都會創建一個新的assemble<BuildTypeName>任務。

`assembleDebug`和`assembleRelease`兩個Task在上面已經提到過，這裡要講這兩個Task從哪裡被創建。當`debug`和`release`構建類型被預創建的時候，它們的tasks就會自動創建對應的這個兩個Task。

上面提到的build.gradle代碼片段中也會實現`assembleJnidebug` task，並且`assemble`會像依賴於`assembleDebug`和`assembleRelease`一樣依賴於`assembleJnidebug`。

提示：你可以在終端下輸入gradle aJ去運行`assembleJnidebug task`。

可能會使用到的情況：

* release模式不需要，只有debug模式下才使用到的權限
* 自定義的debug實現
* 為debug模式使用不同的資源（例如當資源的值由綁定的證書決定）

_BuildType_的代碼和資源通過以下方式被使用：

* manifest將被混合進app的manifest
* 代碼行為只是另一個資源文件夾
* 資源將疊加到main的資源中，並替換已存在的資源。
