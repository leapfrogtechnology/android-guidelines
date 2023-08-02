# Building and Signing apps

## Generating keystore

You do not need Android Studio to sign your app. You can sign your app from the command line using the apksigner tool or configure Gradle to sign it for you during the build. Either way, you need to first generate a private key using keytool.

```
keytool -genkey -v -keystore <name_of_keystore> -keyalg <key_gen_algorithm> -keysize <key_size> -validity <number_of_days> -alias <key_alias>
```

The parameters are as follows:
* name_of_keystore: The keystore file (Eg: leapfrog.jks)
* key_gen_algorithm: Key generation algorithm (Recommended: RSA)
* key_size: Size of keystore file (Recommended: 2048)
* number_of_days: Number of days the certificate will be valid for (Recommended: greater that 25 years, or 10000+)
* key_alias: Alias for key

For example:

```
keytool -genkey -v -keystore my-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-alias
```

You will be asked for additional details like keystore password, key password, certifcate details, etc.

## Signing APKs

Detailed instructions to generate signed apks can be found in the [Android Developer Guidelines](https://developer.android.com/studio/publish/app-signing.html).

It is recommended that you follow the instructions to configure gradle to generate signed apks in the [Gradle Best Practices](Gradle.md).

## Obtaining certificate fingerprint from keystore

SHA-1 certicate is required for a number of purposes (for example, to integrate Google APIs, for uploading to Google Play, etc). You can obtain the certificate fingerprint using the following command:

```
keytool -list -v -keystore {keystore_name} -alias {alias_name}
```

The certificate fingerprints for the debug builds can be obtained using the following command:

#### Mac and Linux
```
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android
```

#### Windows
```
keytool -list -v -keystore "%USERPROFILE%\.android\debug.keystore" -alias androiddebugkey -storepass android -keypass android
```
