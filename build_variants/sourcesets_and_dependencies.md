# Sourcesets and Dependencies（源組件和依賴關係）

與_Build Type_類似，_Product Flavor_也會通過它們自己的_sourceSet_提供代碼和資源。

上面的例子將會創建4個_sourceSet_：

* `android.sourceSets.flavor1`
位於src/flavor1/
* `android.sourceSets.flavor2`
位於src/flavor2/
* `android.sourceSets.androidTestFlavor1`
位於src/androidTestFlavor1/
* `android.sourceSets.androidTestFlavor2`
位於src/androidTestFlavor2/

這些_sourceSet_用於與`android.sourceSets.main`和_Build Type_的_sourceSet_來構建APK。

下面的規則用於處理所有使用的sourceSet來構建一個APK：

* 多個文件夾中的所有的源代碼（src/*/java）都會合並起來生成一個輸出。
* 所有的Manifest文件都會合併成一個Manifest文件。類似於_Build Type_，允許_Product Flavor_可以擁有不同的的組件和權限聲明。
* 所有使用的資源（Android res和assets）遵循的優先級為_Build Type_會覆蓋_Product Flavor_，最終覆蓋`main` _sourceSet_的資源。
* 每一個_Build Variant_都會根據資源生成自己的R類（或者其它一些源代碼）。Variant互相之間沒有什麼是共享的。

最終，類似_Build Type_，_Product Flavor_也可以有它們自己的依賴關係。例如，如果使用flavor來生成一個基於廣告的應用版本和一個付費的應用版本，其中廣告版本可能需要依賴於一個廣告SDK，但是另一個不需要。

    dependencies {
        flavor1Compile "..."
    }

在這個例子中，src/flavor1/AndroidManifest.xml文件中可能需要聲明訪問網絡的權限。

每一個Variant也會創建額外的sourceSet：

* `android.sourceSets.flavor1Debug`
位於src/flavor1Debug/
* `android.sourceSets.flavor1Release`
位於src/flavor1Release/
* `android.sourceSets.flavor2Debug`
位於src/flavor2Debug/
* `android.sourceSets.flavor2Release`
位於src/flavor2Release/

這些sourceSet擁有比Build Type的sourceSet更高的優先級，並允許在Variant的層次上做一些定製。
