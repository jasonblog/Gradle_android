# Manifest entries （Manifest屬性）

通過SDL可以配置一下manifest選項：

* minSdkVersion
* targetSdkVersion
* versionName
* applicationId (有效的包名 -- 更多詳情請查閱[ApplicationId 對比 PackageName](http://tools.android.com/tech-docs/new-build-system/applicationid-vs-packagename))
* package Name for the test application
* Instrumentation test runner

例如：

    android {
        compileSdkVersion 19
        buildToolsVersion "19.0.0"

        defaultConfig {
            versionCode 12
            versionName "2.0"
            minSdkVersion 16
            targetSdkVersion 16
        }
    }

在`android`元素中的`defaultConfig`元素中定義所有配置。

之前的Android Plugin版本使用packageName來配置manifest文件中的packageName屬性。從0.11.0版本開始，你需要在build.gradle文件中使用applicationId來配置manifest文件中的packageName屬性。
這是為了消除應用程序的packageName（也是程序的ID）和java包名所引起的混亂。

在構建文件中定義的強大之處在於它是動態的。
例如，可以從一個文件中或者其它自定義的邏輯代碼中讀取版本信息：


    def computeVersionName() {
        ...
    }

    android {
        compileSdkVersion 19
        buildToolsVersion "19.0.0"

        defaultConfig {
            versionCode 12
            versionName computeVersionName()
            minSdkVersion 16
            targetSdkVersion 16
        }
    }

注意：不要使用與在給定範圍內的getter方法可能引起衝突的方法名。例如，在defaultConfig{...}中調用getVersionName()將會自動調用defaultConfig.getVersionName()方法，你自定義的getVersionName()方法就被取代掉了。

如果一個屬性沒有使用DSL進行設置，一些默認的屬性值將會被使用。以下表格是可能使用到的值：

Property Name      |Default value in DSL object|Default value
-------------      |:-------------:            | -----:
`versionCode`        |-1     |value from manifest if present
`versionName`        |null   |value from manifest if present
`minSdkVersion`	    |-1     |value from manifest if present
`targetSdkVersion`|-1 |value from manifest if present
`applicationId`	    |null   |value from manifest if present
`testApplicationId`  |null   |applicationId + “.test”
`testInstrumentationRunner`  |null|android.test.InstrumentationTestRunner
`signingConfig`      |null   |null
`proguardFile`       |N/A (set only)     |N/A (set only)
`proguardFiles`      |N/A (set only)     |N/A (set only)

如果你在構建腳本中使用自定義代碼邏輯請求這些屬性，那麼第二列的值將非常重要。例如，你可能會寫：

    if (android.defaultConfig.testInstrumentationRunner == null) {
        // assign a better default...
    }

如果這個值一直保持null，那麼在構建執行期間將會實際替換成第三列的默認值。但是在DSL元素中並沒有包含這個默認值，所以，你無法查詢到這個值。
除非是真的需要，這是為了預防解析應用的manifest文件。
