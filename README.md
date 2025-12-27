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
        // =============================
        // Only arm64-v8a ABI (if you have other, change it using docs (https://bit.ly/flutterabifilters)
        // =============================
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

# Now run the code
```flutter
flutter build apk --release --no-shrink
```
this will build apk file, which is way faster and better than ```flutter run```, after build it will be in folder build and something i dont really remember xd
and then, type in the terminal ```adb install path/to/yourapkfile.apk``` and follow the instructions on your phone (make sure installing apps via usb and usb debugging is on)

THANKS! YOUR FLUTTER PROJECT IS NOW RUNNING GOOD ON OLDER HARDWARE!
