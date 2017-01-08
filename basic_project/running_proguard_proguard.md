# Running Proguard（運行 Proguard）

從Gradle Plugin for ProGuard version 4.10之後就開始支持ProGuard。ProGuard插件是自動添加進來的。如果_Build Type_的_runProguard_屬性被設置為true，對應的task將會自動創建。

    android {
        buildTypes {
            release {
                runProguard true
                proguardFile getDefaultProguardFile('proguard-android.txt')
            }
        }

        productFlavors {
            flavor1 {
            }
            flavor2 {
                proguardFile 'some-other-rules.txt'
            }
        }
    }

發佈版本將會使用它的Build Type中聲明的規則文件，product flavor（定製的產品版本）將會使用對應flavor中聲明的規則文件。

這裡有兩個默認的規則文件：

* proguard-android.txt
* proguard-android-optimize.txt

這兩個文件都在SDK的路徑下。使用_getDefaultProguardFile()_可以獲取這些文件的完整路徑。它們除了是否要進行優化之外，其它都是相同的。
