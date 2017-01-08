# Product flavors（不同定製的產品）

一個product flavor定義了從項目中構建了一個應用的自定義版本。一個單一的項目可以同時定義多個不同的flavor來改變應用的輸出。

這個新的設計概念是為了解決不同的版本之間的差異非常小的情況。雖然最項目終生成了多個定製的版本，但是它們本質上都是同一個應用，那麼這種做法可能是比使用庫項目更好的實現方式。

Product flavor需要在`productFlavors`這個DSL容器中聲明：

    android {
        ....

        productFlavors {
            flavor1 {
                ...
            }

            flavor2 {
                ...
            }
        }
    }

這裡創建了兩個flavor，名為`flavor1`和`flavor2`。

---

> 注意：flavor的命名不能與已存在的_Build Type_或者`androidTest`這個_sourceSet_有衝突。
