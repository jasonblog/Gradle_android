# Android tasks

Android plugin使用相同的約定以兼容其他插件，並且附加了自己的標識性task，包括：
* `assemble`
這個task用於組合項目中的所有輸出。
* `check`
這個task用於執行所有檢查。
* `connectedCheck`
這個task將會在一個指定的設備或者模擬器上執行檢查，它們可以同時在所有連接的設備上執行。
* `deviceCheck`
通過APIs連接遠程設備來執行檢查，這是在CL服務器上使用的。
* `build`
這個task執行assemble和check的所有工作。
* `clean`
這個task清空項目的所有輸出。

這些新的標識性task是必須的，以保證能夠在沒有設備連接的情況下執行定期檢查。
注意`build` task不依賴於`deviceCheck`或者`connectedCheck`。

一個Android項目至少擁有兩個輸出：debug APK（調試版APK)和release APK（發佈版APK）。每一個輸出都擁有自己的標識性task以便能夠單獨構建它們。
* `assemble`
    * `assembleDebug`
    * `assembleRelease`

它們都依賴於其它一些tasks以完成構建一個APK需要多個步驟。其中assemble task依賴於這兩個task，所以執行`assemble`將會同時構建出兩個APK。

---

> 小提示：gradle在命令行終端上支持駱駝命名法的task簡稱，例如，執行

>       gradle aR

> 命令等同於執行

>       gradle assembleRelease。

---

check task也擁有自己的依賴：
* `check`
    * `lint`
* `connectedCheck`
    * `connectedAndroidTest`
    * `connectedUiAutomatorTest`(目前還沒有應用到）
* `deviceCheck`
    * 這個test依賴於test創建時，其它實現測試擴展點的插件。

最後，只要task能夠被安裝（那些要求籤名的task），android plugin就會為所有構建類型（`debug`，`release`，`test`）安裝或者卸載。
