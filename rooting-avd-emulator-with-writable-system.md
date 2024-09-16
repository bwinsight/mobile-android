# Rooting AVD emulator with writable system parition

1. Install Android Studio

2. Add a new Android virtual device (AVD): Google Pixel 3a, Android 12 (API 31), select Google Play image.

3. Download the rootAVD script repository to root the AVD with Magisk:
```
git clone https://gitlab.com/newbit/rootAVD.git
```

4. Find and root the selected AVD:
```
./rootAVD.sh ListAllAVDs | grep 31
./rootAVD.sh system-images/android-31/google_apis_playstore/arm64-v8a/ramdisk.img
```

5. Locate the AVD and remount the system partition with write permission:
```
cd ~/Library/Android/sdk/emulator
./emulator -list-avds
./emulator -avd Pixel_3_API_31_Google_Play -writable-system
```

6. Run the following optional commands:
```
adb root
adb remount
```

7. Check if the AVD is rooted:
```
adb shell
su (approve the permission grant screen on the device)
```

8. Open Magisk and reboot the device.
