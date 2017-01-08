# Basics and Configuration（基本知識和配置）

正如前面所提到的，緊鄰`main` _sourceSet_的就是`androidTest` _sourceSet_，默認路徑在src/androidTest/下。
在這個測試_sourceSet_中會構建一個使用Android測試框架，並且可以部署到設備上的測試apk來測試應用程序。這裡麵包含單元測試，集成測試，和後續UI自動化測試。
這個測試sourceSet不應該包含AndroidManifest.xml文件，因為這個文件會自動生成。

下面這些值可能會在測試應用配置中使用到：

* `testPackageName`
* `testInstrumentationRunner`
* `testHandleProfiling`
* `testfunctionalTest`

正如前面所看到的，這些配置在defaultConfig對象中配置：

    android {
        defaultConfig {
            testPackageName "com.test.foo"
            testInstrumentationRunner "android.test.InstrumentationTestRunner"
            testHandleProfiling true
            testFunctionalTest true
        }
    }

在測試應用程序的manifest文件中，instrumentation節點的targetPackage屬性值會自動使用測試應用的package名稱設置，即使這個名稱是通過`defaultConfig`或者_Build Type_對象自定義的。這也是manifest文件需要自動生成的一個原因。

另外，這個測試_sourceSet_也可以擁有自己的依賴。
默認情況下，應用程序和他的依賴會自動添加的測試應用的classpath中，但是也可以通過以下來擴展：

    dependencies {
        androidTestCompile 'com.google.guava:guava:11.0.2'
    }

測試應用通過`assembleTest` task來構建。`assembleTest`不依賴於main中的`assemble` task，需要手動設置運行，不能自動運行。

目前只有一個_Build Type_被測試。默認情況下是`debug` _Build Type_，但是這也可以通過以下自定義配置：

    android {
        ...
        testBuildType "staging"
    }
