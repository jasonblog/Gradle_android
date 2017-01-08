# Manipulation tasks（操作task）

基礎Java項目有一組有限的task用於互相處理生成一個輸出。
`classes`是一個編譯Java源代碼的task。可以在build.gradle文件中通過腳本很容易使用`classes`。這是`project.tasks.classes`的縮寫。

在Android項目中，相比之下這就有點複雜。因為Android項目中會有大量相同的task，並且它們的名字基於_Build Types_和_Product Flavor_生成。

為了解決這個問題，`android`對象有兩個屬性：

* `applicationVariants`（只適用於app plugin）
* `libraryVariants`（只適用於library plugin）
* `testVariants`（兩個plugin都適用）

這三個都會分別返回一個ApplicationVariant、LibraryVariant和TestVariant對象的[DomainObjectCollection](http://www.gradle.org/docs/current/javadoc/org/gradle/api/DomainObjectCollection.html
)。

注意使用這三個collection中的其中一個都會觸發生成所有對應的task。這意味著使用collection之後不需要更改配置。

DomainObjectCollection可以直接訪問所有對象，或者通過過濾器進行篩選。

    android.applicationVariants.each { variant ->
        ....
    }

這三個variant類都共享下面的屬性：

屬性名	       	|屬性類型	    |說明
-------------  	|:-------------:| -----:
name	        |String	|Variant的名字，必須是唯一的。
description		|String	|Variant的描述說明。
dirName	    	|String|Variant的子文件夾名，必須也是唯一的。可能也會有不止一個子文件夾，例如“debug/flavor1”
baseName	    |String	|Variant輸出的基礎名字，必須唯一。
outputFile	    |File	|Variant的輸出，這是一個可讀可寫的屬性。
processManifest	|ProcessManifest	|處理Manifest的task。
aidlCompile		|AidlCompile	|編譯AIDL文件的task。
renderscriptCompile	|RenderscriptCompile    	|編譯Renderscript文件的task。
mergeResources	|MergeResources	|混合資源文件的task。
mergeAssets		|MergeAssets	|混合asset的task。
processResources|ProcessAndroidResources	|處理並編譯資源文件的task。
generateBuildConfig	|GenerateBuildConfig	|生成BuildConfig類的task。
javaCompile		|JavaCompile	|編譯Java源代碼的task。
processJavaResources|Copy	|處理Java資源的task。
assemble		|DefaultTask	|Variant的標誌性assemble task。

ApplicationVariant類還有以下附加屬性：

屬性名			|屬性類型	|說明
-------------  	|:-------------:| -----:
buildType		|BuildType	|Variant的BuildType。
productFlavors	|List<ProductFlavor>	|Variant的ProductFlavor。一般不為空但也允許空值。
mergedFlavor	|ProductFlavor	|android.defaultConfig和variant.productFlavors的合併。
signingConfig	|SigningConfig	|Variant使用的SigningConfig對象。
isSigningReady	|boolean	|如果是true則表明這個Variant已經具備了所有需要簽名的信息。
testVariant		|BuildVariant	|將會測試這個Variant的TestVariant。
dex				|Dex	|將代碼打包成dex的task。如果這個Variant是個庫，這個值可以為空。
packageApplication	|PackageApplication	|打包最終APK的task。如果這個Variant是個庫，這個值可以為空。
zipAlign		|ZipAlign	|zip壓縮APK的task。如果這個Variant是個庫或者APK不能被簽名，這個值可以為空。
install		|DefaultTask	|負責安裝的task，不能為空。
uninstall	|DefaultTask	|負責卸載的task。

LibraryVariant類還有以下附加屬性：

屬性名			|屬性類型	|說明
-------------  	|:-------------:| -----:
buildType		|BuildType	|Variant的BuildType.
mergedFlavor	|ProductFlavor	|The defaultConfig values
testVariant		|BuildVariant	|用於測試這個Variant。
packageLibrary	|Zip	|用於打包庫項目的AAR文件。如果是個庫項目，這個值不能為空。

TestVariant類還有以下屬性：

屬性名			|屬性類型	|說明
-------------  	|:-------------:| -----:
buildType	|BuildType	|Variant的Build Type。
productFlavors	|List<ProductFlavor>	|Variant的ProductFlavor。一般不為空但也允許空值。
mergedFlavor	|ProductFlavor	|android.defaultConfig和variant.productFlavors的合併。
signingConfig	|SigningConfig	|Variant使用的SigningConfig對象。
isSigningReady	|boolean	|如果是true則表明這個Variant已經具備了所有需要簽名的信息。
testedVariant	|BaseVariant	|TestVariant測試的BaseVariant
dex	|Dex	|將代碼打包成dex的task。如果這個Variant是個庫，這個值可以為空。
packageApplication	|PackageApplication	|打包最終APK的task。如果這個Variant是個庫，這個值可以為空。
zipAlign	|ZipAlign	|zip壓縮APK的task。如果這個Variant是個庫或者APK不能被簽名，這個值可以為空。
install	|DefaultTask	|負責安裝的task，不能為空。
uninstall	|DefaultTask	|負責卸載的task。
connectedAndroidTest	|DefaultTask	|在連接設備上行執行Android測試的task。
providerAndroidTest	|DefaultTask	|使用擴展API執行Android測試的task。

Android task特有類型的API：

* ProcessManifest
    * File manifestOutputFile
* AidlCompile
    * File sourceOutputDir
* RenderscriptCompile
    * File sourceOutputDir
    * File resOutputDir
* MergeResources
    * File outputDir
* MergeAssets
    * File outputDir
* ProcessAndroidResources
    * File manifestFile
    * File resDir
    * File assetsDir
    * File sourceOutputDir
    * File textSymbolOutputDir
    * File packageOutputFile
    * File proguardOutputFile
* GenerateBuildConfig
    * File sourceOutputDir
* Dex
    * File outputFolder
* PackageApplication
    * File resourceFile
    * File dexFile
    * File javaResourceDir
    * File jniDir
    * File outputFile
        * 直接在Variant對象中使用“outputFile”可以改變最終的輸出文件夾。
* ZipAlign
    * File inputFile
    * File outputFile
        * 直接在Variant對象中使用“outputFile”可以改變最終的輸出文件夾。

每個task類型的API由於Gradle的工作方式和Android plugin的配置方式而受到限制。
首先，Gradle意味著擁有的task只能配置輸入輸出的路徑和一些可能使用的選項標識。因此，task只能定義一些輸入或者輸出。

其次，這裡面大多數task的輸入都不是單一的，一般都混合了_sourceSet_、_Build Type_和_Product Flavor_中的值。為了保持構建文件的簡單和可讀性，目標是要讓開發者通過DSL語言修改這些對象來配飾構建的過程，而不是深入修改輸入和task的選項。

另外需要注意，除了ZipAlign這個task類型，其它所有類型都要求設置私有數據來讓它們運行。這意味著不可能自動創建這些類型的新task實例。

這些API也可能會被更改。一般來說，目前的API是圍繞著給定task的輸入和輸出入口來添加額外的處理（如果需要的時候）。歡迎反饋意見，特別是那些沒有預見過的需求。

對於Gradle的task（DefaultTask，JavaCompile，Copy，Zip），請參考Gradle文檔。
