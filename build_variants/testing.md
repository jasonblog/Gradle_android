# Testing（測試）

測試multi-flavors項目非常類似於測試簡單的項目。

`androidTest` _sourceSet_用於定義所有flavor共用的測試，但是每一個flavor也可以有它自己特有的測試。

正如前面提到的，每一個flavor都會創建自己的測試sourceSet：

* `android.sourceSets.androidTestFlavor1`
位於src/androidTestFlavor1/
* `android.sourceSets.androidTestFlavor2`
位於src/androidTestFlavor2/

同樣的，它們也可以擁有自己的依賴關係：

    dependencies {
        androidTestFlavor1Compile "..."
    }

這些測試可以通過main的標誌性`deviceCheck` task或者main的`androidTest` task（當flavor被使用的時候這個task相當於一個標誌性task）來執行。

每一個flavor也擁有它們自己的task來這行這些測試：androidTest< VariantName >。例如：

* `androidTestFlavor1Debug`
* `androidTestFlavor2Debug`

同樣的，每一個Variant版本也會創建對應的測試APK構建task和安裝或卸載task：

* `assembleFlavor1Test`
* `installFlavor1Debug`
* `installFlavor1Test`
* `uninstallFlavor1Debug`
* ...

最終的HTML報告支持根據flavor合併生成。
下面是測試結果和報告文件的路徑，第一個是每一個flavor版本的結果，後面的是合併起來的結果：

* build/androidTest-results/flavors/< FlavorName >
* build/androidTest-results/all/
* build/reports/androidTests/flavors< FlavorName >
* build/reports/androidTests/all/
