# Java project tasks（Java項目的Task）

Java plugin主要創建了兩個task，依賴於main task（一個標識性的task）：
* `assemble`
    * `jar`
    這個task創建所有輸出
* `check`
    * `test`
    這個task執行所有的測試。

`jar` task自身直接或者間接依賴於其他task：`classes` task將會被調用於編譯java源碼。
`testClasses` task用於編譯測試，但是它很少被調用，因為`test` task依賴於它（類似於`classes` task）。

通常情況下，你只需要調用到`assemble`和`check`，不需要其他task。

你可以在Gradle文檔中查看[java plugin](http://gradle.org/docs/current/userguide/java_plugin.html)的全部task。
