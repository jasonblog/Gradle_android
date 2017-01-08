# Why Gradle？（為什麼使用gradle）
Gradle是一個優秀的構建系統和構建工具，它允許通過插件創建自定義的構建邏輯。
我們基於Gradle以下的一些特點而選擇了它：

* 採用了Domain Specific Language(DSL語言)來描述和控制構建邏輯。
* 構建文件基於Groovy，並且允許通過混合聲明DSL元素和使用代碼來控制DSL元素以控制自定義的構建邏輯。
* 支持Maven或者Ivy的依賴管理。
* 非常靈活。允許使用最好的實現，但是不會強制實現的方式。
* 插件可以提供自己的DSL和API以供構建文件使用。
* 良好的API工具供IDE集成。
