# Configuring Burp Suite CA as System CA on Android Emulator (using Android 9.0 image)

1. Create a new Android Virtual Device in the Android Device Manager, using the following parameters: 
```
Device: Pixel 4 XL
System image: Android 9.0 Android Open Source Project
API level: API 28
ABI: arm64-v8a
```

2. Run the created device

3. Export the Burp CA Certificate in DER format, then convert it using the following commands:

```
openssl x509 -inform DER -in <exported-burp-ca.der> -out cacert.pem
openssl x509 -inform PEM -subject_hash_old -in cacert.pem |head -1
mv cacert.pem <hash>.0
```

4. Issue the following commands in Terminal (MacOS):

```
cd ~/Library/Android/sdk/emulator
./emulator -list-avds
./emulator -avd Pixel_4_XL_API_28_Rooted_No_Play -writable-system
adb root
adb shell avbctl disable-verification OR adb disable-verity
adb reboot
adb root
adb remount (you might need to reboot again then run adb remount)
adb push <hash>.0 /system/etc/security/cacerts
adb shell chmod 664 /system/etc/security/cacerts/<hash>.0
adb reboot
```

5. The Burp CA (PortSwigger CA) is now installed on the device as system CA:

<img src="https://github.com/bwinsight/mobile-android/assets/55597077/eaf397d6-1078-490a-be1e-05721e76fd5b" width=35% height=35%>

