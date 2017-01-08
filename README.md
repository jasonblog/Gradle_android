Gradle Android插件用戶指南翻譯
---

Gradle Plugin User Guide 官方原文地址  
http://tools.android.com/tech-docs/new-build-system/user-guide

中文版在線閱讀地址  
http://avatarqing.github.io/Gradle-Plugin-User-Guide-Chinese-Verision

GitHub地址  
https://github.com/AvatarQing/Gradle-Plugin-User-Guide-Chinese-Verision

本指南的翻譯內容均出自於CSDN的__琴絃第七__，本人只是對其做出微小修正，對照了英文原文歸納整理成markdown格式的文本並生成gitbook，方便大家閱讀學習。[翻譯原文地址點此打開](http://blog.csdn.net/qinxiandiqi/article/category/2394347)。

---

__琴絃第七__

google推出了全新的Android Studio集成開發環境，其中Android項目的結構與Eclipse的Android項目結構有很大的區別，原因就在於兩開發環境使用的構建工具不同。

Android Studio使用Gradle構建工具，Eclipse的ADT插件使用的是Ant構建工具。因為兩個構建工具的區別，導致習慣了Eclipse開發環境的開發者剛開始比較難適應Android Studio。如果要遷移到Android Studio，建議最好了解下Gradle構建工具。Gradle構建工具是任務驅動型的構建工具，並且可以通過各種Plugin插件擴展功能以適應各種構建任務。對應Android項目的Gradle插件就是Android Gradle Plugin。本文是Google官方的Android Gradle Plugin使用指南翻譯，以方便我大天朝開發者學習。如英語水平還不錯的同學，建議直接查看官方原文，本人的理解和翻譯難免有所疏漏。

---

License

採用[知識共享 署名-非商業性使用-相同方式共享 4.0 國際 許可協議](http://creativecommons.org/licenses/by-nc-sa/4.0/)進行許可。


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/AvatarQing/gradle-plugin-user-guide-chinese-verision/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

