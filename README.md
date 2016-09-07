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
    initUI();
  } else{
    ActivityCompat.requestPermissions(this,new String[]{Manifest.permission.CAMERA, Manifest.permission.WRITE_EXTERNAL_STORAGE},MY_CODE);
  }
}

@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, int[] grantResults){
  super.onRequestPermissionsResult(requestCode,permissions, grantResults);
  if(requstCode == MY_CODE){
    if(grantResults[0]=PackageManager.PERMISSION_GRANTED && grantResults[1]=PackageManager.PERMISSION_GRANTED){
      initUI();
    }else{
      Toast.makeText(this,"",Toast.LENGTH_SHORT).show();
    }
  }
}
```
#####2
######1
activity_main.xml
```
<TextureView
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:id="@+id/preview"
  android:layout_centerInParent="true"
  />
<android.support.design.widget.FloatingActionButton
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:src="@drawable/ic_camera_alt_black_24dp"
  android:tint="@android:color/white"
  android:id="@+id/fab"
  android:layout_alignParentBottom="true"
  android:layout_alignParentRight="true"
  android:layout_marginRight="@dimen/activity_horizontal_margin"
  android:layout_marginBottom="@dimen/activity_vertical_margin"
  />
```
MainActivity.java
```
private CameraManager cm;
private CameraDevice cd;
private CameraCaptureSession ccs;
private Handler h;
private int previewWidth =640;
private int previewHeight =480;
private String backCamera;

//

private void initCamera(){
  cm = (CameraManager)getSystemService(CAMERA_SERVICE);
  try{
    String[] cameras = cm.getCameraIdList();
    for(String c:cameras){
      CameraCharacteristics ccc = cm.getCameraCharacteristics(c);
      if(ccc.get(CameraCharacteristics.LENS_FACING)==CameraCharacteristics.LENS_FACING_BACK){
        backCamera=c;
        return;
      }
    }
  }catch(CameraAccessException e){
    e.printStackTrace();
  }
}


private void initPreview(){
  try{
    int orient = cm.getCameraCharacteristics(backCamera).get(CameraCharacteristics.SENSOR_ORIENTATION);]
    preview.getLayoutParams().width = previewHeight;
    preview.getLayoutParams().height = previewWidth;
    preview.requestLayout();
    
    preview.setSurfaceTextureListener(new TextureView.SurfaceTextureListener(){
      @Override
      public void onSurfaceTextureAvailable(SurfaceTexture surfaceTexture int i){
        startPreview();
      }
    )}
  }catch(CameraAccessException e){
  }
}
```
