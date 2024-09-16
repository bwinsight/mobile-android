# Rooting AVD emulator with writable system parition

1. Install Android Studio.

2. Add a new Android virtual device (AVD): Google Pixel 3a, Android 12 (API 31), select **Google Play** image.

3. Set Edit / Show Advanced Settings / Cold boot option.

4. Launch the AVD and login to the Play Store, keep the AVD running.

5. Download the rootAVD script repository to root the AVD with Magisk:
```
git clone https://gitlab.com/newbit/rootAVD.git
```

6. Find and root the selected AVD:
```
./rootAVD.sh ListAllAVDs | grep 31
./rootAVD.sh system-images/android-31/google_apis_playstore/arm64-v8a/ramdisk.img
```

7. Locate the AVD and remount the system partition with write permission:
```
cd ~/Library/Android/sdk/emulator
./emulator -list-avds
./emulator -avd Pixel_3_API_31_Google_Play -writable-system
```

8. Check if the AVD is rooted:
```
adb shell
su (approve the permission grant screen on the device)
```

9. Open Magisk and reboot the device.

# Install Burp CA certificate as system CA

1. Export the CA in DER format, rename it to burp.crt and copy to the AVD:
```
adb push burp.crt /sdcard/Download
```

2. Install the certificate as User certificate: Settings / Security / Encryption & Credentials / Install a certificate / CA certificate / INSTALL ANYWAY / browse Downloads / burp.crt

3. Check if the certificate is installed: Settings / Security / Encryption & Credentials / Trusted credentials / USER
<img src="https://github.com/user-attachments/assets/457ee974-9c0e-4db5-92d2-5e99b06b0d74" width=25% height=25%>

4. Install Always Trust User Certificates Magisk module:
```
wget https://github.com/NVISOsecurity/MagiskTrustUserCerts/releases/download/v0.4.1/AlwaysTrustUserCerts.zip
adb push AlwaysTrustUserCerts.zip / sdcard/Download
```
Open Magisk app on the AVD / Modules / Install from Storage / Downloads / AlwaysTrustUserCerts.zip / Reboot

5. Check if Burp CA is installed as system CA: Settings / Security / Encryption & Credentials / Trusted credentials / SYSTEM
<img src="https://github.com/user-attachments/assets/3cec218a-e9e1-4b15-8185-c14e8f02eb17" width=25% height=25%>
