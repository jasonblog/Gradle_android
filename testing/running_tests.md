# Running tests（運行測試）

正如前面提到的，標誌性task `connectedCheck`要求一個連接的設備來啟動。
這個過程依賴於`androidTest` task，因此將會運行`androidTest`。這個task將會執行下面內容：

* 確認應用和測試應用都被構建（依賴於`assembleDebug`和`assembleTest`）。
* 安裝這兩個應用。
* 運行這些測試。
* 卸載這兩個應用。

如果有多於一個連接設備，那麼所有測試都會同時運行在所有連接設備上。如果其中一個測試失敗，不管是哪一個設備算失敗。

所有測試結果都被保存為XML文檔，路徑為：

    _build/androidTest-results_

（這類似於JUnit的運行結果保存在build/test-results)

同樣，這也可以自定義配置：

    android {
        ...

        testOptions {
            resultsDir = "$project.buildDir/foo/results"
        }
    }

這裡的`android.testOptions.resultsDir`將由`Project.file(String)`獲得。
