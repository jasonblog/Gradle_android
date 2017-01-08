# Project Structure（項目結構）

上面提到的基本的構建文件需要一個默認的文件夾結構。Gradle遵循約定優先於配置的概念，在可能的情況儘可能提供合理的默認配置參數。

基本的項目開始於兩個名為“source sets”的組件，即main source code和test code。它們分別位於：

 * src/main/
 * src/androidTest/

裡面每一個存在的文件夾對應相應的源組件。
對於Java plugin和Android plugin來說，它們的Java源代碼和資源文件路徑如下：

* java/
* resources/

但對於Android plugin來說，它還擁有以下特有的文件和文件夾結構：

* AndroidManifest.xml
* res/
* assets/
* aidl/
* rs/
* jni/

---

> 注意：src/androidTest/AndroidManifest.xml是不需要的，它會自動被創建。

---
