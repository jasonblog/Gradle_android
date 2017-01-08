# Multi-projects reports（多項目報告）

在一個配置了多個應用或者多個庫項目的多項目裡，當同時運行所有測試的時候，生成一個報告文件記錄所有的測試可能是非常有用的。

為了實現這個目的，需要使用同一個依賴文件（譯註：指的是使用android gradle插件的依賴文件）中的另一個插件。可以通過以下方式添加：

    buildscript {
        repositories {
            mavenCentral()
        }

        dependencies {
            classpath 'com.android.tools.build:gradle:0.5.6'
        }
    }
    
    apply plugin: 'android-reporting'

這必須添加到項目的根目錄下，例如與settings.gradle文件同個目錄的build.gradle文件中。

之後，在命令行中導航到項目根目錄下，輸入以下命令就可以運行所有測試併合並所有報告：

    gradle deviceCheck mergeAndroidReports --continue

---

> 注意：這裡的--continue選項將允許所有測試，即使子項目中的任何一個運行失敗都不會停止。如果沒有這個選項，第一個失敗測試將會終止全部測試的運行，這可能導致一些項目沒有執行過它們的測試。

---
