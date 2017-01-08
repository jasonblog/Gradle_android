# Build Variants（構建變種版本）

新構建系統的一個目標就是允許為同一個應用創建不同的版本。

這裡有兩個主要的使用情景：

1. 同一個應用的不同版本。
例如一個免費的版本和一個收費的專業版本。
2. 同一個應用需要打包成不同的apk以發佈Google Play Store。
[點擊此處][1]查看更多詳細信息。
3. 綜合1和2兩種情景。

這個目標就是要讓在同一個項目裡生成不同的APK成為可能，以取代以前需要使用一個庫項目和兩個及兩個以上的應用項目分別生成不同APK的做法。

[1]: http://developer.android.com/google/play/publishing/multiple-apks.html
