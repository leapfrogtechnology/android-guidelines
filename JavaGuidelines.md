# Java Guidelines

## File Structure

A source file consists of, in order:

* License or copyright information, if present
* Package statement
* Import statements
* Exactly one top-level class
* Exactly one blank line separates each section that is present.


### Import Statements Order

Because we use Android Studio, so imports should always be ordered automatically. However, in the case that they may not be, then they should be ordered as follows:

1. Android imports
2. Imports from third parties
3. java and javax imports
4. Imports from the current Project

**Note:**

- Imports should be alphabetically ordered within each grouping, with capital letters before lower case letters (e.g. Z before a)
- There should be a blank line between each major grouping (android, com, JUnit, net, org, java, javax)

### Class member ordering

The ordering of the members of a class can have a great effect on learnability, but there is no single correct recipe for how to do it but using a logical and consistent order will improve code learnability and readability. It is recommendable to use the following order:

1. Constants
2. Fields
3. Constructors
4. Override methods and callbacks (public or private)
5. Public methods
6. Private methods
7. Inner classes or interfaces

#### Field Ordering

Any fields declared at the top of a class file should be ordered in the following order:

1. Enums
2. Constants
3. Dagger Injected fields
4. Butterknife View Bindings
5. private global variables
6. public global variables

For example:

```java
    public static enum {
      ENUM_ONE, ENUM_TWO
    }

    public static final String KEY_NAME = "KEY_NAME";
    public static final int COUNT_USER = 0;

    @Inject SomeAdapter someAdapter;

    @BindView(R.id.text_name) TextView nameTextView;
    @BindView(R.id.image_photo) ImageView photoImageView;

    private int userCount;
    private String errorMessage;

    public int someCount;
    public String someString;
```

Using this ordering convention helps to keep field declarations grouped, which increases both the locating of and readability of said fields.

#### Class member ordering

To improve code readability, it’s important to organise class members in a logical manner. The following order should be used to achieve this:


1. Constants
2. Fields
3. Constructors
4. Override methods and callbacks (public or private)
5. Public methods
6. Private methods
7. Inner classes or interfaces

For example:

```java
    public class MainActivity extends Activity {

        private int count;

        public static newInstance() { }

        @Override
        public void onCreate() { }

        public setUsername() { }

        private void setupUsername() { }

        static class AnInnerClass { }

        interface SomeInterface { }

    }
```

Any lifecycle methods used in Android framework classes should be ordered in the corresponding lifecycle order. For example:

```java
    public class MainActivity extends Activity {

        // Field and constructors

        @Override
        public void onCreate() { }

        @Override
        public void onStart() { }

        @Override
        public void onResume() { }

        @Override
        public void onPause() { }

        @Override
        public void onStop() { }

        @Override
        public void onRestart() { }

        @Override
        public void onDestroy() { }

        // public methods, private methods, inner classes and interfaces

    }
```

**Note:**
When a class has multiple constructors, or multiple methods with the same name, these appear sequentially, with no intervening members (not even private ones).

##### Method parameter ordering

When defining methods, parameters should be ordered to the following convention:

```java
    public Post loadPost(Context context, int postId);

    public void loadPost(Context context, int postId, Callback callback);
```

**Context** parameters always go first and **Callback** parameters always go last.


## Naming Conventions

### Class File Naming

Class names are written in __UpperCamelCase__.

For classes that extend an Android component, the name of the class should end with the name of the component; for example: `SignInActivity`, `SignInFragment`, `ImageUploaderService`, `ChangePasswordDialog`.

### Variable Naming

All fields should be declared at the top of the file, following these rules:

- Private, non-static field names should not start with m. This is right:

  `userSignedIn`, `userNameText`, `acceptButton`

Not this:

  `mUserSignedIn`, `mUserNameText`, `mAcceptButton`

Private, static field names do not need to start with an s. This is right:

  `someStaticField`, `userNameText`

Not this:
  `sSomeStaticField`, `sUserNameText`

- All other fields also start with a lower case letter.

```java
      int numOfChildren;
      String username;
```

- Static final fields (known as constants) are ALL_CAPS_WITH_UNDERSCORES.

```java
      private static final int PAGE_COUNT = 0;
```

Field names that do not reveal intention should not be used. For example,

```java
    int e; //number of elements in the list
```

why not just give the field a meaningful name in the first place, rather than leaving a comment!

```java
    int numberOfElements;
```

That's much better!

#### View Field Naming

When naming fields that reference views, the name of the view should be the last word in the name. When naming fields that reference viewgroups, suffix the variable name with __Layout__. For example:

| View           | Name                   |
|----------------|------------------------|
| TextView       | usernameTextView       |
| Button         | acceptLoginButton      |
| ImageView      | profileAvatarImageView |
| RelativeLayout | profileLayout          |

We name views in this way so that we can easily identify what the field corresponds to. For example, having a field named **user** is extremely ambiguous - giving it the name usernameTextView, userImageView or userProfileLayout helps to make it clear  exactly what view the field corresponds with.

#### Avoid naming with container types

Leading on from the above, we should also avoid the use of container type names when creating variables for collections. For example, say we have an `ArrayList` containing a list of userIds:

Do:
```java
    List<String> userIds = new ArrayList<>();
```

Don't:
```java
    List<String> userIdList = new ArrayList<>();
```

If and when container names change in the future, the naming of these can often get forgotten about - and just like view naming, it's not entirely necessary. Correct naming of the container itself should provide enough information for what it is.

#### Avoid similar naming

Naming variables, method and / or classes with similar names can make it confusing for other developers reading over your code. For example:

```
    hasUserSelectedSingleProfilePreviously

    hasUserSelectedSignedProfilePreviously
```

Distinguishing the difference between these at a first glance can be hard to understand what is what. Naming these in a clearer way can make it easier for developers to navigate the fields in your code.

#### Number series naming

When Android Studio auto-generates code for us, it's easy to leave things as they are - even when it generate horribly named parameters! For example, this isn't very nice:

```java
    public void doSomething(String s1, String s2, String s3)
```

It's hard to understand what these parameters do without reading the code. Instead:

```java
    public void doSomething(String userName, String userEmail, String userId)
```

That makes it much easier to understand! Now we'll be able to read the code following the parameter with a much clearer understanding 🙂

#### Pronounceable names

When naming fields, methods and classes they should:

- Be readable: Efficient naming means we'll be able to look at the name and understand it instantly, reducing cognitive load on trying to decipher what the name means.

- Be speakable: Names that are speakable avoids awkward conversations where you're trying to pronounce a badly named variable name.

- Be searchable: Nothing is worse than trying to search for a method or variable in a class to realise it's been spelt wrong or badly named. If we're trying to find a method that searches for a user, then searching for 'search' should bring up a result for that method.

- Not use Hungarian notation: Hungarian notation goes against the three points made above, so it should never be used!

#### Treat acronyms as words

Any acronyms for class names, variable names etc should be treated as words - this applies for any capitalisation used for any of the letters. For example:

| Do              | Don't           |
|-----------------|-----------------|
| setUserId       | setUserID       |
| String uri      | String URI      |
| int id          | int ID          |
| parseHtml       | parseHTML       |
| generateXmlFile | generateXMLFile |


#### String constants, naming and values

When using string constants, they should be declared as `static final` and use the follow conventions:


| Element            | Field Name Prefix   |
| -----------------  | ------------------- |
| SharedPreferences  | `PREF_`             |
| Bundle             | `BUNDLE_`           |
| Fragment Arguments | `ARG_`              |
| Intent Extra       | `EXTRA_`            |
| Intent Action      | `ACTION_`           |
| Request Code       | `RC_`               |

Note that the arguments of a Fragment - `Fragment.getArguments()` - are also a Bundle. However, because this is a quite common use of Bundles, we define a different prefix for them.

Example:

```java
// Note the value of the field is the same as the name to avoid duplication issues
static final String PREF_EMAIL = "PREF_EMAIL";
static final String BUNDLE_AGE = "BUNDLE_AGE";
static final String ARG_USER_ID = "ARG_USER_ID";

// Intent-related items use full package name as value
static final String EXTRA_SURNAME = "com.myapp.extras.EXTRA_SURNAME";
static final String ACTION_OPEN_USER = "com.myapp.action.ACTION_OPEN_USER";
```



## Best Practices

#### Avoid justifying variable declarations

Any declaration of variables should not use any special form of alignment, for example:

This is fine:

```java
    private int userId = 8;
    private int count = 0;
    private String username = "hitherejoe";
```

Avoid doing this:

```java
    private String username = "hitherejoe";
    private int userId      = 8;
    private int count       = 0;
```

This creates a stream of whitespace which is known to make text difficult to read for certain learning difficulties.

#### Use spaces for indentation

For blocks, 4 space indentation should be used:

```java
    if (userSignedIn) {
        count = 1;
    }
```

Whereas for line wraps, 8 spaces should be used:

```java
    String userAboutText =
            "This is some text about the user and it is pretty long, can you see!";
```

### Limit line length

Code lines should exceed no longer than 100 characters, this makes the code more readable. Sometimes to achieve this, we may need to:

- Extract data to a local variable
- Extract logic to an external method
- Line-wrap code to separate a single line of code to multiple lines

**Note:** For code comments and import statements it’s ok to exceed the 100 character limit.

#### Line-wrapping techniques

When it comes to line-wraps, there’s a few situations where we should be consistent in the way we format code.

**Breaking at Operators**

When we need to break a line at an operator, we break the line before the operator:

```java
    int count = countOne + countTwo - countThree + countFour * countFive - countSix
            + countOnANewLineBecauseItsTooLong;
```

If desirable, you can always break after the `=` sign:

```java
    int count =
            countOne + countTwo - countThree + countFour * countFive + countSix;
```

**Method Chaining**

When it comes to method chaining, each method call should be on a new line.

Don’t do this:

```java
    Picasso.with(context).load("someUrl").into(imageView);
```

Instead, do this:

```java
    Picasso.with(context)
            .load("someUrl")
            .into(imageView);
```

**Long Parameters**

In the case that a method contains long parameters, we should line break where appropriate. For example when declaring a method we should break after the last comma of the parameter that fits:

```java
    private void someMethod(Context context, String someLongStringName, String text,
                                long thisIsALong, String anotherString) {               
    }             
```

And when calling that method we should break after the comma of each parameter:

```java
    someMethod(context,
            "thisIsSomeLongTextItsQuiteLongIsntIt",
            "someText",
            01223892365463456,
            "thisIsSomeLongTextItsQuiteLongIsntIt");
```

#### No line-wrapping for imports

Import statements are not line-wrapped. The column limit (Column limit: 100) does not apply to import statements.

### Method spacing

There only needs to be a single line space between methods in a class, for example:

Do this:

```java
    public String getUserName() {
        // Code
    }

    public void setUserName(String name) {
        // Code
    }

    public boolean isUserSignedIn() {
        // Code
    }
```

Not this:

```java
    public String getUserName() {
        // Code
    }


    public void setUserName(String name) {
        // Code
    }


    public boolean isUserSignedIn() {
        // Code
    }
```

### Comments

#### Inline comments

Where necessary, inline comments should be used to provide a meaningful description to the reader on what a specific piece of code does. They should only be used in situations where the code may be complex to understand. In most cases however, code should be written in a way that it easy to understand without comments 🙂

**Note:** Code comments do not have to, but should try to, stick to the 100 character rule.

#### JavaDoc style Comments

Whilst a method name should usually be enough to communicate a methods functionality, it can sometimes help to provide JavaDoc style comments. This helps the reader to easily understand the methods functionality, as well as the purpose of any parameters that are being passed into the method.

```java
    /**
     * Authenticates the user against the API given a User id.
     * If successful, this returns a success result
     *
     * @param userId The user id of the user that is to be authenticated.
     */
```

#### Class comments

When creating class comments they should be meaningful and descriptive, using links where necessary. For example:

```java
    /**
      * RecyclerView adapter to display a list of {@link Post}.
      * Currently used with {@link PostRecycler} to show the list of Post items.
      */
```

Don’t leave author comments, these aren’t useful and provide no real meaningful information when multiple people are to be working on the class.

```java
    /**
      * Created By Joe 18/06/2016
      */
```

### TODO

Use TODO comments for code that is temporary, a short-term solution, or good-enough but not perfect. TODOs should include the string TODO in all caps, followed by a colon:

```java
// TODO: Remove this code after the UrlTable2 has been checked in.
```
and

```java
// TODO: Change this to use a flag instead of a constant.
```
If your TODO is of the form "At a future date do something" make sure that you either include a very specific date ("Fix by November 2005") or a very specific event ("Remove this code after all production mixers understand protocol V7.").

### Sectioning code

If creating ‘sections’ for code, this should be done using the following approach, like this:

```java
    public void method() { }

    public void someOtherMethod() { }

    /********* Mvp Method Implementations  ********/

    public void anotherMethod() { }

    /********* Helper Methods  ********/

    public void someMethod() { }
```

Not like this:

```java
    public void method() { }

    public void someOtherMethod() { }

    // Mvp Method Implementations

    public void anotherMethod() { }
```

This makes sectioned methods easier to located in a class.


### Exceptions

#### Don’t ignore exceptions
Avoid not handling exceptions in the correct manner. For example:

```java
	public void setUserId(String id) {
    	try {
        	mUserId = Integer.parseInt(id);
    	} catch (NumberFormatException e) { }
	}
```

This gives no information to both the developer and the user, making it harder to debug and could also leave the user confused if something goes wrong. When catching an exception, we should also always log the error to the console for debugging purposes and if necessary alert the user of the issue. For example:

```java
	public void setCount(String count) {
    	try {
        	count = Integer.parseInt(id);
    	} catch (NumberFormatException e) {
    		count = 0;
        	Log.e(TAG, "There was an error parsing the count " + e);
        	DialogFactory.showErrorMessage(R.string.error_message_parsing_count);
    	}
	}
```

Here we handle the error appropriately by:

- Showing a message to the user notifying them that there has been an error
- Setting a default value for the variable if possible
- Throw an appropriate exception

#### Don’t catch generic exception

Catching exceptions generally should not be done:

```java
	public void openCustomTab(Context context, Uri uri) {
    	Intent intent = buildIntent(context, uri);
    	try {
        	context.startActivity(intent);
    	} catch (Exception e) {
        	Log.e(TAG, "There was an error opening the custom tab " + e);
    	}
	}
```

Why?

*Do not do this. In almost all cases it is inappropriate to catch generic Exception or Throwable (preferably not Throwable because it includes Error exceptions). It is very dangerous because it means that Exceptions you never expected (including RuntimeExceptions like ClassCastException) get caught in application-level error handling. It obscures the failure handling properties of your code, meaning if someone adds a new type of Exception in the code you're calling, the compiler won't help you realize you need to handle the error differently. In most cases you shouldn't be handling different types of exception the same way.* - taken from the Android Code Style Guidelines

Instead, catch the expected exception and handle it accordingly:

```java
    public void openCustomTab(Context context, Uri uri) {
      Intent intent = buildIntent(context, uri);
      try {
          context.startActivity(intent);
      } catch (ActivityNotFoundException e) {
          Log.e(TAG, "There was an error opening the custom tab " + e);
      }
    }
```

#### Grouping Exceptions

Where exceptions execute the same code, they should be grouped in-order to increase readability and avoid code duplication. For example, where you may do this:

```java
    public void openCustomTab(Context context, @Nullable Uri uri) {
      Intent intent = buildIntent(context, uri);
      try {
          context.startActivity(intent);
      } catch (ActivityNotFoundException e) {
          Log.e(TAG, "There was an error opening the custom tab " + e);
      } catch (NullPointerException e) {
          Log.e(TAG, "There was an error opening the custom tab " + e);
      } catch (SomeOtherException e) {
        // Show some dialog
        }
    }
```

You could do this:

```java
    public void openCustomTab(Context context, @Nullable Uri uri) {
      Intent intent = buildIntent(context, uri);
      try {
          context.startActivity(intent);
      } catch (ActivityNotFoundException e | NullPointerException e) {
          Log.e(TAG, "There was an error opening the custom tab " + e);
      } catch (SomeOtherException e) {
        // Show some dialog
        }
    }
```

#### Using try-catch over throw exception

Using try-catch statements improves the readability of the code where the exception is taking place. This is because the error is handled where it occurs, making it easier to both debug or make a change to how the error is handled.

#### Don’t use finalizers

Finalizers are a way to have a chunk of code executed when an object is garbage collected. While they can be handy for doing cleanup (particularly of external resources), there are no guarantees as to when a finalizer will be called (or even that it will be called at all).

Android doesn't use finalizers. In most cases, you can do what you need from a finalizer with good exception handling. If you absolutely need it, define a close() method (or the like) and document exactly when that method needs to be called (see InputStream for an example). In this case it is appropriate but not required to print a short log message from the finalizer, as long as it is not expected to flood the logs.

### Import statements

#### Use fully qualify imports

When you want to use class Bar from package foo,there are two possible ways to import it:

```java
    import foo.*;
```

Potentially reduces the number of import statements.

```java
    import foo.Bar;
```

Makes it obvious what classes are actually used and the code is more readable for maintainers.

An explicit exception is made for java standard libraries (java.util.\*, java.io.\*, etc.) and unit test code (junit.framework.\*).

### Remove Unused Elements

All unused fields, imports, methods and classes should be removed from the code base unless there is any specific reasoning behind keeping it there.

### If-statements

#### Use standard brace style

Braces should always be used on the same line as the code before them. For example, avoid doing this:

```java
    class SomeClass
    {
      private void someFunction()
      {
          if (isSomething)
          {

          }
          else if (!isSomethingElse)
          {

          }
          else
          {

          }
      }
    }
```

And instead, do this:

```java
    class SomeClass {
      private void someFunction() {
          if (isSomething) {

          } else if (!isSomethingElse) {

          } else {

          }
      }
    }
```

Not only is the extra line for the space not really necessary, but it makes blocks easier to follow when reading the code.

#### Inline if-clauses

Sometimes it makes sense to use a single line for if statements. For example:

```java
    if (user == null) return false;
```

However, it only works for simple operations. Something like this would be better suited with braces:

```java
    if (user == null) throw new IllegalArgumentExeption("Oops, user object is required.");
```

#### Nested if-conditions

Where possible, if-conditions should be combined to avoid over-complicated nesting. For example:

Do:

```java
    if (userSignedIn && userId != null) {

    }
```

Try to avoid:

```java
    if (userSignedIn) {
        if (userId != null) {

        }
    }
```

This makes statements easier to read and removes the unnecessary extra lines from the nested clauses.

#### Ternary Operators

Where appropriate, ternary operators can be used to simplify operations.

For example, this is easy to read:

```java
    userStatusImage = signedIn ? R.drawable.ic_tick : R.drawable.ic_cross;
```

and takes up far fewer lines of code than this:

```java
    if (signedIn) {
        userStatusImage = R.drawable.ic_tick;
    } else {
        userStatusImage = R.drawable.ic_cross;
    }
```

**Note:** There are some times when ternary operators should not be used. If the if-clause logic is complex or a large number of characters then a standard brace style should be used.

### Annotations

#### Annotation practices

Taken from  the Android code style guide:

**@Override:** The `@Override` annotation must be used whenever a method overrides the declaration or implementation from a super-class. For example, if you use the `@inheritdocs` Javadoc tag, and derive from a class (not an interface), you must also annotate that the method `@Overrides` the parent class's method.

**@SuppressWarnings:** The `@SuppressWarnings` annotation should only be used under circumstances where it is impossible to eliminate a warning. If a warning passes this "impossible to eliminate" test, the `@SuppressWarnings` annotation must be used, so as to ensure that all warnings reflect actual problems in the code.

Annotations should always be used where possible. For example, using the `@Nullable` annotation should be used in cases where a field could be expected as null. For example:

```java
    @Nullable
    TextView userNameTextView;

    private void getName(@Nullable String name) { }
```

#### Annotation style

Annotations that are applied to a method or class should always be defined in the declaration, with only one per line and each field separated by a blank line:

```java
    @Bind(R.id.layout_coordinator)
    CoordinatorLayout coordinatorLayout;

    @Bind(R.id.layout_coordinator)
    CoordinatorLayout coordinatorLayout;

    @Inject
    MainPresenter mainPresenter;

    @Annotation
    @AnotherAnnotation
    public class SomeClass {

      @SomeAnotation
      public String getMeAString() {

      }

    }
```

### Logging

Logging should be used to log useful error messages and/or other information that may be useful during development.


| Log                               | Reason      |
|-----------------------------------|-------------|
| Log.v(String tag, String message) | verbose     |
| Log.d(String tag, String message) | debug       |
| Log.i(String tag, String message) | information |
| Log.w(String tag, String message) | warning     |
| Log.e(String tag, String message) | error       |


We can set the `Tag` for the log as a `static final` field at the top of the class, for example:

```java
    private static final String TAG = MyActivity.class.getName();
```

All verbose and debug logs must be disabled on release builds. On the other hand - information, warning and error logs should only be kept enabled if deemed necessary.

```java
    if (BuildConfig.DEBUG) {
        Log.d(TAG, "Here's a log message");
    }
```

**Note:** __Timber__ is the preferred logging method to be used. It handles the tagging for us, which saves us keeping a reference to a TAG. It also helps in ignoring logs for release builds.

### Avoid using Enums

Enums should only be used where actually required. If another method is possible, then that should be the preferred way of approaching the implementation. For example:

Instead of this:

```java
    public enum SomeEnum {
        ONE, TWO, THREE
    }
```

Do this:

```java
    private static final int VALUE_ONE = 1;
    private static final int VALUE_TWO = 2;
    private static final int VALUE_THREE = 3;
```

### Passing data in Activities and Fragments

When we pass data using an Intent or Bundle, the keys for the values must use the conventions defined below:

**Activity**

Passing data to an activity must be done using a reference to a KEY, as defined as below:

```java
    private static final String EXTRA_NAME = "com.your.package.name.to.activity.KEY_NAME";
```

**Fragment**

Passing data to a fragment must be done using a reference to an EXTRA, as defined as below:

```java
    private static final String ARG_NAME = "EXTRA_NAME";
```

When creating new instances of a fragment or activity that involves passing data, we should provide a static method to retrieve the new instance, passing the data as method parameters. For example:

**Activity**

```java
    public static Intent getLaunchIntent(Context context, Post post) {
        Intent intent = new Intent(context, CurrentActivity.class);
        intent.putParcelableExtra(EXTRA_POST, post);
        return intent;
    }
```

**Fragment**

```java
    public static PostFragment newInstance(Post post) {
        PostFragment fragment = new PostFragment();
        Bundle args = new Bundle();
        args.putParcelable(ARG_POST, post);
        fragment.setArguments(args)
        return fragment;
    }
```

### Limit variable scope

The scope of local variables should be kept to a minimum (Effective Java Item 29). By doing so, you increase the readability and maintainability of your code and reduce the likelihood of error. Each variable should be declared in the innermost block that encloses all uses of the variable.

Local variables should be declared at the point they are first used. Nearly every local variable declaration should contain an initializer. If you don't yet have enough information to initialize a variable sensibly, you should postpone the declaration until you do. - taken from the Android code style guidelines

### Force non-instantiability

If you do not want an object to be created using the new keyword, enforce it using a private constructor. Especially useful for utility classes that contain only static functions.

```java
class DateTimeUtils {

    /**
     * Prevents instantiation
     **/
    private DateTimeUtils() {}

    static String formatDate(Date date) {
        // ...
    }
}
```
