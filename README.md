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
To support API 23,  
MainActivity.java
```
private static final int MY_CODE =1;
onCreate(BUndle savedInstanceState){
  request()
}

private void request(){
  if(ContextCompat.checkSelfPermission(this,Mainfest.permission.CAMERA)==PackageManager.PERMISSION_GRANTED)&&
  ContextCompat.checkSelfPermission(this,Mainfest.permission.WRITE_EXTERNAL_STORAGE)==PackageManager.PERMISSION_GRANTED){
    
  } else{
    ActivityCompat.requestPermissions(this,new String[]{Manifest.permission.CAMERA, Manifest.permission.WRITE_EXTERNAL_STORAGE},MY_CODE);
  }
}

@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, int[] grantResults){
  super.onRequestPermissionsResult(requestCode,permissions, grantResults);
  if(requstCode == MY_CODE){
    if(grantResults[0]=PackageManager.PERMISSION_GRANTED && grantResults[1]=PackageManager.PERMISSION_GRANTED){
      
    }else{
      Toast.makeText(this,"",Toast.LENGTH_SHORT).show();
    }
  }
}
```
