# Configuring the Structure

當默認的項目結構不適用的時候，你可能需要去配置它。根據Gradle文檔，重新為Java項目配置_sourceSets_可以使用以下方法：

    sourceSets {
        main {
            java {
                srcDir 'src/java'
            }
            resources {
                srcDir 'src/resources'
            }
        }
    }

---

> 注意：`srcDir`將會被添加到指定的已存在的源文件夾中（這在Gradle文檔中沒有提到，但是實際上確實會這樣執行）。

---

替換默認的源代碼文件夾，你可能想要使用能夠傳入一個路徑數組的`srcDirs`來替換單一的`srcDir`。以下是使用調用對象的另一種不同方法：

    sourceSets {
        main.java.srcDirs = ['src/java']
        main.resources.srcDirs = ['src/resources']
    }

想要獲取更多信息，可以參考Gradle文檔中關於[Java Pluign](http://gradle.org/docs/current/userguide/java_plugin.html)的部分。

Android Plugin使用的是類似的語法。但是由於它使用的是自己的_sourceSets_，這些配置將會被添加在`android`對象中。

以下是一個示例，它使用了舊項目結構中的main源碼，並且將`androidTest` _sourceSet_組件重新映射到_tests_文件夾。

    android {
        sourceSets {
            main {
                manifest.srcFile 'AndroidManifest.xml'
                java.srcDirs = ['src']
                resources.srcDirs = ['src']
                aidl.srcDirs = ['src']
                renderscript.srcDirs = ['src']
                res.srcDirs = ['res']
                assets.srcDirs = ['assets']
            }

            androidTest.setRoot('tests')
        }
    }

---

> 注意：由於舊的項目結構將所有的源文件（java,aidl,renderscripthe和java資源文件）都放在同一個目錄裡面，所以我們需要將這些_sourceSet_組件重新映射到`src`目錄下。

---

> 注意：`setRoot()`方法將移動整個組件（包括它的子文件夾）到一個新的文件夾。示例中將會移動`src/androidTest/*`到`tests/*`下。
以上這些是Android特有的，如果配置在Java的_sourceSets_裡面將不會有作用。

---

以上也是將舊構建系統項目遷移到新構建系統需要做的遷移工作。
