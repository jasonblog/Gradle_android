# Build Type  + Product Flavor = Build Variant（構建類型+定製產品=構建變種版本）

正如前面章節所提到的，每一個_Build Type_都會生成一個新的APK。

_Product Flavor_同樣也會做這些事情：項目的輸出將會拼接所有可能的_Build Type_和_Product Flavor_（如果有Flavor定義存在的話）的組合。

每一種組合（包含_Build Type_和_Product Flavor_）就是一個_Build Variant_（構建變種版本）。

例如，在上面的Flavor聲明例子中與默認的`debug`和`release`兩個_Build Type_將會生成4個_Build Variant_：

* Flavor1 - debug
* Flavor1 - release
* Flavor2 - debug
* Flavor2 - release

項目中如果沒有定義flavor同樣也會有_Build Variant_，只是使用的是默認的flavor和配置。`default`(默認)的flavor/config是沒有名字的，所以生成的Build Variant列表看起來就跟_Build Type_列表一樣。
