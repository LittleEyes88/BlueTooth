# BlueTooth
经测试，目前可连接锤子手机，SONY SRS-XB10音箱。

1. 设计蓝牙为可见:
Intent intent = new Intent(BluetoothAdapter.ACTION_REQUEST_DISCOVERABLE);
     intent.putExtra(BluetoothAdapter.EXTRA_DISCOVERABLE_DURATION, 180);//180可见时间
     startActivity(intent);
2. 关闭蓝牙:
     /**关闭蓝牙*/
     if (mBluetoothAdapter.isEnabled()) {
           mBluetoothAdapter.disable();
     }
     
3.Android 6.0的系统需要动态添加权限才能搜索出蓝牙设备
Android 6.0的系统需要动态添加权限

    /**判断手机系统的版本*/
    if (Build.VERSION.SDK_INT >= 6.0) {//Build.VERSION.SDK_INT >= Build.VERSION_CODES.M
            if(ActivityCompat.checkSelfPermission(this,Manifest.permission.ACCESS_COARSE_LOCATION)!=PackageManager.PERMISSION_GRANTED){
                /**动态添加权限：ACCESS_FINE_LOCATION*/
                ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.ACCESS_FINE_LOCATION},
                        MY_PERMISSION_REQUEST_CONSTANT);
            }
        }
        
        
    请求权限的回调
    /**请求权限的回调：这里判断权限是否添加成功*/
     /**请求权限的回调：这里判断权限是否添加成功*/
    public void onRequestPermissionsResult(int requestCode, String permissions[], int[] grantResults) {
        switch (requestCode) {
            case MY_PERMISSION_REQUEST_CONSTANT: {
                if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                    Log.i("main","添加权限成功");
                }
                return;
            }
        }
    }
4.参考链接：
http://blog.csdn.net/u012987546/article/details/52204542
https://developer.android.com/guide/topics/connectivity/bluetooth.html?hl=zh-cn
