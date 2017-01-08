# Differences between a Project and a Library Project（普通項目和庫項目之間的區別）

一個庫項目的main輸出是一個.aar包（它代表Android的歸檔文件）。它組合了編譯代碼（例如jar包或者是本地的.so文件）和資源（manifest，res，assets）。
一個庫項目同樣也可以獨立於應用程序生成一個測試用的apk來測試。

標識Task同樣適用於庫項目（`assembleDebug`，`assembleRelease`），因此在命令行上與構建一個項目沒有什麼不同。

其餘的部分，庫項目與應用程序項目一樣。它們都擁有build type和product flavor，也可以生成多個aar版本。
記住大部分Build Type的配置不適用於庫項目。但是你可以根據庫項目是否被其它項目使用或者是否用來測試來使用自定義的sourceSet改變庫項目的內容。
