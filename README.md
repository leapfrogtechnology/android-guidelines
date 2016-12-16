# Android Coding Standard

##### 2.2.24.3 RxJava chains styling

When chaining Rx operations, every operator should be on a new line, breaking the line before the period `.` . For example:

    return dataManager.getPost()
                .concatMap(new Func1<Post, Observable<? extends Post>>() {
                    @Override
                     public Observable<? extends Post> call(Post post) {
                         return mRetrofitService.getPost(post.id);
                     }
                })
                .retry(new Func2<Integer, Throwable, Boolean>() {
                     @Override
                     public Boolean call(Integer numRetries, Throwable throwable) {
                         return throwable instanceof RetrofitError;
                     }
                });

This makes it easier to understand the flow of operation within an Rx chain of calls.

#### 2.2.25 Butterknife

##### 2.2.25.1 Event listeners

Where possible, make use of Butterknife listener bindings. For example, when listening for a click event instead of doing this:

    mSubmitButton.setOnClickListener(new View.OnClickListener() {
        public void onClick(View v) {
            // Some code here...
        }
      };

Do this:

    @OnClick(R.id.button_submit)
    public void onSubmitButtonClick() { }


### 2.4 Test style rules

#### 2.4.1 Unit tests

Any Unit Test classes should be written to match the name of the class that the test are targeting, followed by the Test suffix. For example:

| Class                | Test Class               |
|----------------------|--------------------------|
| DataManager          | DataManagerTest          |
| UserProfilePresenter | UserProfilePresenterTest |
| PreferencesHelper    | PreferencesHelperTest    |

All Test methods should be annotated with the `@Test` annotation, the methods should be named using the following template:

    @Test
    public void methodNamePreconditionExpectedResult() { }

So for example, if we want to check that the signUp() method with an invalid email address fails, the test would look like:

    @Test
    public void signUpWithInvalidEmailFails() { }

Tests should focus on testing only what the method name entitles, if there’s extra conditions being tested in your Test method then this should be moved to it’s own individual test.

If a class we are testing contains many different methods, then the tests should be split across multiple test classes - this helps to keep the tests more maintainable and easier to locate. For example, a DatabaseHelper class may need to be split into multiple test classes such as :

    DatabaseHelperUserTest
    DatabaseHelperPostsTest
    DatabaseHelperDraftsTest

#### 2.4.2 Espresso tests

Each Espresso test class generally targets an Activity, so the name given to it should match that of the targeted Activity, again followed by Test. For example:

| Class                | Test Class               |
|----------------------|--------------------------|
| MainActivity         | MainActivityTest         |
| ProfileActivity      | ProfileActivityTest      |
| DraftsActivity       | DraftsActivityTest       |

When using the Espresso API, methods should be chained on new lines to make the statements more readable, for example:

    onView(withId(R.id.text_title))
            .perform(scrollTo())
            .check(matches(isDisplayed()))

Chaining calls in this style not only helps us stick to less than 100 characters per line but it also makes it easy to read the chain of events taking place in espresso tests.

## 3. Being consistent

Our parting thought: BE CONSISTENT. If you're edition code, take a few minutes to look at the code around you and determine its style. If they use spaces around if clauses, you should too. If their comments have little boxes of stars around them, make your comments have little boxes of stars around them too.

The point of having style guidelines is to have a common vocabulary of coding, so people can concentrate on what you're saying, rather than on how you're saying it. We present global style rules here so people know the vocabulary. But local style is also important. If code you add to a file looks drastically different from the existing code around it, it throws readers our of their rhythm when they to to read it.

### 4.2 MVP Architecture

A brief case study for the Model View Presenter (MVP) Architecture while we were developing apps for the Android Platform is described [here] (https://gist.github.com/grishmashrestha/cefe04eeaf74091fb80d66d6c13631b1).

## 5. Sources
- https://github.com/futurice/android-best-practices#gradle-configuration (Prefer to follow this)
- https://lftechnology.atlassian.net/wiki/display/AS/Android+Station
- https://github.com/bufferapp/android-guidelines/blob/master/project_style_guidelines.md
- https://google.github.io/styleguide/javaguide.html
- http://source.android.com/source/code-style.html
- https://github.com/ribot/android-guidelines/blob/master/architecture_guidelines/android_architecture.md
- http://tools.android.com/tech-docs/new-build-system/user-guide
- https://developer.android.com/studio/projects/index.html
- https://github.com/ribot/android-guidelines/edit/master/project_and_code_guidelines.md
- https://medium.com/rocknnull/effective-java-for-android-cheatsheet-bf4e3433889a#.2p879tgbo
