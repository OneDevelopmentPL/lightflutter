# Light Flutter (for devices with 8GB RAM)
Flutter conifguration for older devices to run smoothly

## 1.  Edit ```gradle.properties``` file in your flutter project
Then, add/replace with this:
```gradle.propeties
# ===============================
# Gradle JVM settings (lightweight)
# ===============================
# Heap max 1.5 GB, metaspace 512 MB, dump when OOM
org.gradle.jvmargs=-Xmx1536M -XX:MaxMetaspaceSize=512m -XX:+HeapDumpOnOutOfMemoryError

# ===============================
# AndroidX
# ===============================
android.useAndroidX=true

# ===============================
# Compilation parallel off for older CPUs
# ===============================
org.gradle.parallel=false

# ===============================
# Cache = on
# ===============================
org.gradle.caching=true

# ===============================
# Logs for memory
# ===============================
org.gradle.debug=true
```

## 2. Edit ```build.gradle.kts``` in ```android/app/build.gradle.kts```
ADD/EDIT!! DO NOT PASTE FULLY!
```build.gradle.kts
...
android {
    defaultConfig {
        ...
        ndk {
            biFilters.add("arm64-v8a")
        }
    }
    buildTypes {
        release {
            ...
            signingConfig = signingConfigs.getByName("debug")
        }
        debug {
           ...
        }
    }
...
}
```
