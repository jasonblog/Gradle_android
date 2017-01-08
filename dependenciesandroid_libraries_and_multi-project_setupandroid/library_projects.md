# Library projects（庫項目）

在上面的多項目配置中，`:libraries:lib1`和`:libraries:lib2`可能是一個Java項目，並且`:app`這個Android項目將會使用它們的jar包輸出。

但是，如果你想要共享代碼來訪問Android API或者使用Android樣式的資源，那麼這些庫就不能是通常的Java項目，而應該是Android庫項目。
