# Multi project setup（多項目設置）

Gradle項目也可以通過使用多項目配置依賴於其它Gradle項目。

多項目配置的實現通常是在一個根項目路徑下將所有項目作為子文件夾包含進去。


例如，給定以下項目結構：

    MyProject/
     + app/
     + libraries/
        + lib1/
        + lib2/

我們可以定義3個項目。Grand將會按照以下名字映射它們：

    :app
    :libraries:lib1
    :libraries:lib2

每一個項目都擁有自己的build.gradle文件來聲明自己如何構建。
另外，在根目錄下還有一個_setting.gradle_文件用於聲明所有項目。
這些文件的結構如下：

    MyProject/
     | settings.gradle
     + app/
        | build.gradle
     + libraries/
        + lib1/
           | build.gradle
        + lib2/
           | build.gradle

其中setting.gradle的內容非常簡單：

    include ':app', ':libraries:lib1', ':libraries:lib2'

這裡定義了哪一個文件夾才是真正的Gradle項目。

其中`:app`項目可能依賴於這些庫，這是通過以下依賴配置聲明的：

    dependencies {
        compile project(':libraries:lib1')
    }

更多關於多項目配置的信息請參考[這裡][1]。

[1]: http://gradle.org/docs/current/userguide/multi_project_builds.html
