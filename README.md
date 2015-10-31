# gtlib
OneGlove is a gesture based remote smartphone control product. This SDK provides the necessary libraries required to operate OneGlove on Android 4.4 and above operated smartphones.

# Setting Up Your Environment

1) Create a new Android Studio Project with minimum SDK version 4.4 Kit Kat.

2) Clone the One Glove SDK from “ https://github.com/rizasif/OneGlove ” (or download as Zip file and unzip it).

3) In your Android Studio Project go to “File -> Import Module”, Select "Import .JAR or .AAR Package" option and under File Name provide link to "gtlib-release.aar" file in your cloned/downloaded folder.

4) In build.gradle (Module: app) add the following code to dependencies:

    
    compile project(':gtlib-release')
    
    
5) In the App Manifest add the following permissions:

    
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
    <uses-feature android:name="android.hardware.bluetooth_le" android:required="true"/>
    
    
6) In the App Manifest add the following code to your   <Application>   cell (e.g   <Application> CODE
GOES HERE </Application>    ):
    
    <service android:name="gestech.com.gtlib.Bluetooth.BluetoothLeServices" />
    <receiver android:name="gestech.com.gtlib.GestechInterfaces.GtBroadcastReceiver">
        <intent-filter>
            <action android:name="com.rfduino.ACTION_CONNECTED" />
            <action android:name="com.rfduino.ACTION_DISCONNECTED" />
            <action android:name="com.rfduino.ACTION_DATA_AVAILABLE" />
        </intent-filter>
    </receiver>
    
    
    
# Starting Gesture Recognition

7) Use “implements GtHelper” in your activity class

8) Create and initialize an object of class 'OneGlove' in onCreate() method and provide the required arguments (Note: Device name is provided along with product).

    
    //Initializing global variable oneGlove
    oneGlove = new OneGlove(Device_Name, bluetoothAdapter, this);
    
    
9) Register callback functions in your Acticity:

    
    oneGlove.registerCallBack(this, this);
    
    
10) Finally put the SDK to scan for your device:

    
    oneGlove.beginScan();
    
    
11. View your desired gesture in onGestureAnalyzed() callback method, produced as a result of GtHelper implementation i.e String gesture contains the name of detected gesture.


# Note:


1) To disconnect a device use:

    
    oneGlove.disconnect();
    
    
2) To obtain connection status at anytime use:

    
    oneGlove.getStatus();
    
    
3) To add custom gestures, perform a gesture and in "onGestureReceived(AccelerometerData gesture)" callback method write the following code (you may name your new gesture by any String):

    
    gesture.set_name("*Your_New_Gesture_Name*");
    oneGlove.addCustomGesture(gesture);
    
    
4) To delete a custom gesture:

    
    oneGlove.deleteGesture("*Your_Gesture_Name*");
    
    
5) To view all stored gestures:

    
    List<AccelerometerData> gestureList = oneGlove.getAllGestures();
    for (AccelerometerData gesture : gestureList){
        Log.i("Gestures: ", gesture.get_name());    //Prints in logcat
    }
    
    
