# Library Publication（庫項目發佈）

一般情況下一個庫只會發佈它的_release_ Variant（變種）版本。這個版本將會被所有引用它的項目使用，而不管它們本身自己構建了什麼版本。這是由於Gradle的限制，我們正在努力消除這個問題，所以這只是臨時的限制。

你可以控制哪一個Variant版本作為發行版：

    android {
        defaultPublishConfig "debug"
    }

注意這裡的發佈配置名稱引用的是完整的Variant版本名稱。_Relesae_，_debug_只適用於項目中沒有其它特性版本的時候使用。如果你想要使用其它Variant版本取代默認的發佈版本，你可以：

    android {
        defaultPublishConfig "flavor1Debug"
    }

將庫項目的所有Variant版本都發布也是可能的。我們計劃在一般的項目依賴項目（類似於上述所說的）情況下允許這種做法，但是由於Gradle的限制（我們也在努力修復這個問題）現在還不太可能。
默認情況下沒有啟用發佈所有Variant版本。可以通過以下啟用：

    android {
        publishNonDefault true
    }

理解發布多個Variant版本意味著發佈多個arr文件而不是一個arr文件包含所有Variant版本是非常重要的。每一個arr包都包含一個單一的Variant版本。
發佈一個變種版本意味著構建一個可用的arr文件作為Gradle項目的輸出文件。無論是發佈到一個maven倉庫，還是其它項目需要創建一個這個庫項目的依賴都可以使用到這個文件。

Gradle有一個默認文件的概念。當添加以下配置後就會被使用到：

    compile project(':libraries:lib2')

創建一個其它發佈文件的依賴，你需要指定具體使用哪一個：

    dependencies {
        flavor1Compile project(path: ':lib1', configuration: 'flavor1Release')
        flavor2Compile project(path: ':lib1', configuration: 'flavor2Release')
    }

---

> 重要：注意已發佈的配置是一個完整的Variant版本，其中包括了build type，並且需要像以上一樣被引用。

---

> 重要：當啟用非默認發佈，maven發佈插件將會發布其它Variant版本作為擴展包（按分類器分類）。這意味著不能真正的兼容發佈到maven倉庫。你應該另外發佈一個單一的Variant版本到倉庫中，或者允許發佈所有配置以支持跨項目依賴。

---
