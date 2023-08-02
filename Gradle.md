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

Instead, make a `keystore.properties` file which should _not_ be added to the version control system:

```
    storePassword=test123
    keyPassword=test1234
    keyAlias=sch
    storeFile=/Users/ayush/sch.keystore
```

To import the properties for build configuration follow the steps listed below:

i. In your module's build.gradle file, add code to load your keystore.properties file before the android {} block.

```groovy
    ...

    // Create a variable called keystorePropertiesFile, and initialize it to your
    // keystore.properties file, in the rootProject folder.
    def keystorePropertiesFile = rootProject.file("keystore.properties")

    // Initialize a new Properties() object called keystoreProperties.
    def keystoreProperties = new Properties()

    // Load your keystore.properties file into the keystoreProperties object.
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))

    android {
        ...
    }
```

Note: You could choose to store your keystore.properties file in another location (for example, in the module folder rather than the root folder for the project, or on your build server if you are using a continuous integration tool). In that case, you should modify the code above to correctly initialize keystorePropertiesFile using your actual keystore.properties file's location.

ii. You can refer to properties stored in `keystoreProperties` using the syntax `keystoreProperties['propertyName']`. Modify the `signingConfigs` block of your module's `build.gradle` file to reference the signing information stored in keystoreProperties using this syntax.

```groovy
    android {
        signingConfigs {
            config {
                keyAlias keystoreProperties['keyAlias']
                keyPassword keystoreProperties['keyPassword']
                storeFile file(keystoreProperties['storeFile'])
                storePassword keystoreProperties['storePassword']
            }
        }
        ...
    }
```
