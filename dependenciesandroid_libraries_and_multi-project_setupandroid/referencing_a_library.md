# Referencing a Library（引用一個庫項目）

引用一個庫項目的方法與引用其它項目的方法一樣：

    dependencies {
        compile project(':libraries:lib1')
        compile project(':libraries:lib2')
    }

---

> 注意：如果你要引用多個庫，那麼排序將非常重要。這類似於舊構建系統裡面的project.properties文件中的依賴排序。

---
