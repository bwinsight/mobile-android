# Converting Android App Bundle (AAB) to Android Package (APKS) file

1. Obtain Google's [BundleTool](https://github.com/google/bundletool).

2. Create a new keystore:
```
keytool -genkey -v -keystore my-key.keystore -alias my-key -keyalg RSA -keysize 2048 -validity 10000
```

3. Covert AAB file to APKS file and resign (keystore's password was `12345678`):
```
java -jar bundletool-all.jar build-apks --bundle="Android-application.aab" --output="Android-application.apks" --ks=my-key.keystore --ks-pass=pass:12345678 --ks-key-alias=my-key --key-pass=pass:12345678
```

4. Install the APKS file on the Android device:
```
java -jar bundletool-all.jar install-apks --apks="Android-application.apks"
```
