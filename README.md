#### tptakepicandroidapp
#####1
######1
create empty activity.  
in AndroidManifest.xml
```
<uses-permission android:name="android.permission.CAMERA"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>

<activity android:name=".MainActivity" android.screenOrientation="potrait">
</activity>
```

build.gradle
```
compile 'com.android.support:design:23.1.1'
compile 'jp.co.cyberagent.android.gpuimage:gpuimage-library:1.4.1'
```

[android-gpuimage](https://github.com/CyberAgent/android-gpuimage)
