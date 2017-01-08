# Single projects（獨立項目）

一個項目將會自動生成測試運行。默認位置為：build/reports/androidTests

這非常類似於JUnit的報告所在位置build/reports/tests，其它的報告通常位於build/reports/< plugin >/。

這個路徑也可以通過以下方式自定義：

    android {
        ...

        testOptions {
            reportDir = "$project.buildDir/foo/report"
        }
    }

報告將會合並運行在不同設備上的測試結果。
