# Multi-flavor variants

在一些情況下，一個應用可能需要基於多個標準來創建多個版本。例如，Google Play中的multi-apk支持4個不同的過濾器。區分創建的不同APK的每一個過濾器要求能夠使用多維的Product Flavor。

假如有個遊戲需要一個免費版本和一個付費的版本，並且需要在multi-apk支持中使用ABI過濾器（譯註：ABI，應用二進制接口，優點是不需要改動應用的任何代碼就能夠將應用遷移到任何支持相同ABI的平臺上）。這個遊戲應用需要3個ABI和兩個特定應用版本，因此就需要生成6個APK（沒有因計算不同_Build Types_生成的Variant版本）。
然而，注意到在這個例子中，為三個ABI構建的付費版本源代碼都是相同，因此創建6個flavor來實現不是一個好辦法。
相反的，使用兩個flavor維度，並且自動構建所有可能的Variant組合。

這個功能的實現就是使用Flavor Groups。每一個Group代表一個維度，並且flavor都被分配到一個指定的Group中。

    android {
        ...

        flavorGroups "abi", "version"

        productFlavors {
            freeapp {
                flavorGroup "version"
                ...
            }

            x86 {
                flavorGroup "abi"
                ...
            }

            ...
        }
    }

`andorid.flavorGroups`數組按照先後排序定義了可能使用的group。每一個_Product Flavor_都被分配到一個group中。

上面的例子中將_Product Flavor_分為兩組（即兩個維度），為別為abi維度[x86,arm,mips]和version維度[freeapp,paidapp]，再加上默認的_Build Type_有[debug,release]，這將會組合生成以下的Build Variant：

* x86-freeapp-debug
* x86-freeapp-release
* arm-freeapp-debug
* arm-freeapp-release
* mips-freeapp-debug
* mips-freeapp-release
* x86-paidapp-debug
* x86-paidapp-release
* arm-paidapp-debug
* arm-paidapp-release
* mips-paidapp-debug
* mips-paidapp-release

`android.flavorGroups`中定義的group排序非常重要（Variant命名和優先級等）。

每一個Variant版本的配置由幾個`Product Flavor`對象決定：

* android.defaultConfig
* 一個來自abi組中的對象
* 一個來自version組中的對象

flavorGroups中的排序決定了哪一個flavor覆蓋哪一個，這對於資源來說非常重要，因為一個flavor中的值會替換定義在低優先級的flavor中的值。

flavor groups使用最高的優先級定義，因此在上面例子中的優先級為：

    abi > version > defaultConfig

Multi-flavors項目同樣擁有額外的sourceSet，類似於Variant的sourceSet，只是少了Build Type：

* `android.sourceSets.x86Freeapp`
位於src/x86Freeapp/
* `android.sourceSets.armPaidapp`
位於src/armPaidapp/
* 等等...

這允許在flavor-combination的層次上進行定製。它們擁有過比基礎的flavor sourceSet更高的優先級，但是優先級低於Build Type的sourceSet。
