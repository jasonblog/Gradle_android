# dex options（dex選項）

    android {
        dexOptions {
            incremental false

            preDexLibraries = false

            jumboMode = false

        }
    }

這將應用所有使用dex的task。
