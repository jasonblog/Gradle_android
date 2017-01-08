# General Tasks（通用任務）

添加一個插件到構建文件中將會自動創建一系列構建任務(build tasks)去執行（注：gradle屬於任務驅動型構建工具，它的構建過程是基於Task的）。Java plugin和Android plugin都會創建以下task：

* `assemble`
這個task將會組合項目的所有輸出。

* `check`
這個task將會執行所有檢查。

* `build`
這個task將會執行assemble和check兩個task的所有工作

* `clean`
這個task將會清空項目的輸出。

實際上`assemble`，`check`，`build`這三個task不做任何事情。它們只是一個Task標誌，用來告訴android plugin添加實際需要執行的task去完成這些工作。

這就允許你去調用相同的task，而不需要考慮當前是什麼類型的項目，或者當前項目添加了什麼plugin。
例如，添加了_findbugs_ plugin將會創建一個新的task並且讓`check` task依賴於這個新的task。當`check` task被調用的時候，這個新的task將會先被調用。

在命令行環境中，你可以執行以下命令來獲取更多高級別的task：

    gradle tasks

查看所有task列表和它們之間的依賴關係可以執行以下命令：

    gradle tasks --all

---

> 注意：Gradle會自動監視一個task聲明的所有輸入和輸出。
兩次執行`build` task並且期間項目沒有任何改動，gradle將會使用UP-TO-DATE通知所有task。這意味著第二次build執行的時候不會請求任何task執行。這允許task之間互相依賴，而不會導致不需要的構建請求被執行。

---
