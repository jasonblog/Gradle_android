# Product Flavor Configuration（Product Flavor的配置）

每一個flavor都是通過閉包來配置的：

    android {
        ...

        defaultConfig {
            minSdkVersion 8
            versionCode 10
        }

        productFlavors {
            flavor1 {
                packageName "com.example.flavor1"
                versionCode 20
            }

            flavor2 {
                packageName "com.example.flavor2"
                minSdkVersion 14
            }
        }
    }

注意_ProductFlavor_類型的`android.productFlavors.*`對象與`android.defaultConfig`對象的類型是相同的。這意味著它們共享相同的屬性。

`defaultConfig`為所有的flavor提供基本的配置，每一個flavor都可以重設這些配置的值。在上面的例子中，最終的配置結果將會是：

    * `flavor1`
        * `packageName`: com.example.flavor1
        * `minSdkVersion`: 8
        * `versionCode`: 20
    * `flavor2`
        * `packageName`: com.example.flavor2
        * `minSdkVersion`: 14
        * `versionCode`: 10

通常情況下，_Build Type_的配置會覆蓋其它的配置。例如，_Build Type_的`packageNameSuffix`會被追加到_Product Flavor_的`packageName`上面。

也有一些情況是一些設置可以同時在_Build Type_和_Product Flavor_中設置。在這種情況下，按照個別為主的原則決定。

例如，`signingConfig`就這種屬性的一個例子。
`signingConfig`允許通過設置`android.buildTypes.release.signingConfig`來為所有的`release`包共享相同的_SigningConfig_。也可以通過設置`android.productFlavors.*.signingConfig`來為每一個release包指定它們自己的_SigningConfig_。
