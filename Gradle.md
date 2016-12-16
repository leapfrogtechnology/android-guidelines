# Gradle

## Best Practices

### Storing sensitive data on a local file and not pushing in a git repo
**Passwords.** In your app's `build.gradle` you will need to define the `signingConfigs` for the release build. Here is what you should avoid:

_Don't do this_. This would appear in the version control system.

```groovy
signingConfigs {
    release {
        storeFile file("myapp.keystore")
        storePassword "password123"
        keyAlias "thekey"
        keyPassword "password789"
    }
}
```

Instead, make a `gradle.properties` file which should _not_ be added to the version control system:

```
KEYSTORE_PASSWORD=password123
KEY_PASSWORD=password789
```

That file is automatically imported by Gradle, so you can use it in `build.gradle` as such:

```groovy
signingConfigs {
    release {
        try {
            storeFile file("myapp.keystore")
            storePassword KEYSTORE_PASSWORD
            keyAlias "thekey"
            keyPassword KEY_PASSWORD
        }
        catch (ex) {
            throw new InvalidUserDataException("You should define KEYSTORE_PASSWORD and KEY_PASSWORD in gradle.properties.")
        }
    }
}
```
