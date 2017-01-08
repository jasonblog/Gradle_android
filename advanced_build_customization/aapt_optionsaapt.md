# aapt options（aapt選項）

    android {
        aaptOptions {
            noCompress 'foo', 'bar'
            ignoreAssetsPattern "!.svn:!.git:!.ds_store:!*.scc:.*:<dir>_*:!CVS:!thumbs.db:!picasa.ini:!*~"
        }
    }

這將影響所有使用aapt的task。
