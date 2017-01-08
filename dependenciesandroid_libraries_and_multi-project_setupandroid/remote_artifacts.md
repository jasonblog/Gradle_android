# Remote artifacts（遠程文件）

Gradle支持從Maven或者Ivy倉庫中拉取文件。

首先必須將倉庫添加到列表中，然後必須在依賴中聲明Maven或者Ivy聲明的文件。

    repositories {
        mavenCentral()
    }


    dependencies {
        compile 'com.google.guava:guava:11.0.2'
    }

    android {
        ...
    }

---

> 注意：`mavenCentral()`是指定倉庫URL的簡單方法。Gradle支持遠程和本地倉庫。

---

> 注意：Gradle會遵循依賴關係的傳遞性。這意味著如果一個依賴本身依賴於其它東西，這些東西也會一併被拉取回來。

---

更多關於設置依賴關係的信息，請參考[Gradle用戶指南][1]和[DSL][2]文檔。

[1]: http://gradle.org/docs/current/userguide/artifact_dependencies_tutorial.html
[2]: http://gradle.org/docs/current/dsl/org.gradle.api.artifacts.dsl.DependencyHandler.html
