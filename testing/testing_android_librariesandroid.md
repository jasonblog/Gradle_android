# Testing Android Libraries（測試Android庫）

測試Android庫項目的方法與應用項目的方法類似。

唯一的不同在於整個庫（包括它的依賴）都是自動作為依賴庫被添加到測試應用中。結果就是測試APK不單隻包含它的代碼，還包含了庫項目自己和庫的所有依賴。
庫的manifest被組合到測試應用的manifest中（作為一些項目引用這個庫的殼）。

`androidTest` task的變改只是安裝（或者卸載）測試APK（因為沒有其它APK被安裝）。

其它的部分都是類似的。
