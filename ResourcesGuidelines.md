# Resource Conventions

## animator

## anim

## color

## drawable

### File Naming

Naming conventions for drawables:

| Asset Type   | Prefix            |    Example                  |
|--------------| ------------------|-----------------------------|
| Action bar   | `ab_`             | `ab_stacked.9.png`          |
| Button       | `btn_`            | `btn_send_pressed.9.png`    |
| Dialog       | `dialog_`         | `dialog_top.9.png`          |
| Divider      | `divider_`        | `divider_horizontal.9.png`  |
| Icon         | `ic_`             | `ic_star.png`               |
| Menu         | `menu_ `          | `menu_submenu_bg.9.png`     |
| Notification | `notification_`   | `notification_bg.9.png`     |
| Tabs         | `tab_`            | `tab_pressed.9.png`         |

Naming conventions for icons (taken from [Android iconography guidelines](http://developer.android.com/design/style/iconography.html)):

| Asset Type                      | Prefix             | Example                      |
| --------------------------------| ----------------   | ---------------------------- |
| Icons                           | `ic_`              | `ic_star.png`                |
| Launcher icons                  | `ic_launcher`      | `ic_launcher_calendar.png`   |
| Menu icons and Action Bar icons | `ic_menu`          | `ic_menu_archive.png`        |
| Status bar icons                | `ic_stat_notify`   | `ic_stat_notify_msg.png`     |
| Tab icons                       | `ic_tab`           | `ic_tab_recent.png`          |
| Dialog icons                    | `ic_dialog`        | `ic_dialog_info.png`         |

Naming conventions for selector states:

| State        | Suffix          | Example                     |
|--------------|-----------------|-----------------------------|
| Normal       | `_normal`       | `btn_order_normal.9.png`    |
| Pressed      | `_pressed`      | `btn_order_pressed.9.png`   |
| Focused      | `_focused`      | `btn_order_focused.9.png`   |
| Disabled     | `_disabled`     | `btn_order_disabled.9.png`  |
| Selected     | `_selected`     | `btn_order_selected.9.png`  |


## mipmap

## menu

## layout

### File Naming

Layout files should match the name of the Android components that they are intended for but moving the top level component name to the beginning. For example, if we are creating a layout for the `SignInActivity`, the name of the layout file should be `activity_sign_in.xml`.

| Component        | Class Name             | Layout Name                   |
| ---------------- | ---------------------- | ----------------------------- |
| Activity         | `UserProfileActivity`  | `activity_user_profile.xml`   |
| Fragment         | `SignUpFragment`       | `fragment_sign_up.xml`        |
| Dialog           | `ChangePasswordDialog` | `dialog_change_password.xml`  |
| AdapterView item | ---                    | `item_person.xml`             |
| Partial layout   | ---                    | `partial_stats_bar.xml`       |

A slightly different case is when we are creating a layout that is going to be inflated by an `Adapter`, e.g to populate a `ListView`. In this case, the name of the layout should start with `item_`.

Note that there are cases where these rules will not be possible to apply. For example, when creating layout files that are intended to be part of other layouts. In this case you should use the prefix `partial_`.

### Id naming

All IDs should be prefixed using the name of the element that they have been declared for.

| Element        | Prefix         |
|----------------|----------------|
| ViewGroup      | layout_        |
| Fragment       | fragment_      |
| ImageView      | imageview_     |
| Button         | button_        |
| TextView       | textview_      |
| EditText         | edittext_      |
| View           | view_          |
| ProgressBar    | progressbar_   |  

For example:

```xml
    <TextView
        android:id="@+id/textview_username"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />
```

Views that typically are only one per layout, such as a toolbar, can simply be given the id of it's view type. E.g.```toolbar```.

### Attributes ordering

Ordering attributes not only looks tidy but it helps to make it quicker when looking for attributes within layout files. As a general rule,

    1. View Id
    2. Style
    3. Layout width and layout height
    4. Other `layout_` attributes, sorted alphabetically
    5. Remaining attributes, sorted alphabetically

For example:

```xml
    <Button
        android:id="@id/button_accept"
        style="@style/ButtonStyle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_alignParentStart="true"
        android:padding="16dp"
        android:text="@string/button_skip_sign_in"
        android:textColor="@color/bluish_gray" />
```

Note: This formatting can be carried out by using the format feature in android studio -

`cmd + shift + L`

Doing this makes it easy to navigate through XML attributes when it comes to making changes to layout files.

## menu

### File Naming

Similar to layout files, menu files should match the name of the component preceded by `menu_`. For example, if we are defining a menu file that is going to be used in the `UserActivity`, then the name of the file should be `menu_activity_user.xml`

## raw

## values

### File Naming

Resource files in the values folder should be __plural__, e.g. `strings.xml`, `styles.xml`, `colors.xml`, `dimens.xml`, `attrs.xml`

## strings.xml

#### String name

All string names should begin with a prefix for the part of the application that they are being referenced from. For example:

| Screen                | String         | Resource Name             |
|-----------------------|----------------|---------------------------|
| Registration Fragment | “Register now” | registration_register_now |
| Sign Up Activity      | “Cancel”       | sign_up_cancel            |
| Rate App Dialog       | “No thanks”    | rate_app_no_thanks        |

If it’s not possible to name the referenced like the above, we can use the following rules:

| Prefix  | Description                                  |
|---------|----------------------------------------------|
| error_  | Used for error messages                      |
| title_  | Used for dialog titles                       |
| action_ | Used for option menu actions                 |
| msg_    | Used for generic message such as in a dialog |
| label_  | Used for activity labels                     |
| button_ | Used for button text                         |
| hint_   | Used for hint                                |
| desc_   | Used for image descriptions                  |

Two important things to note for String resources:

 - String resources should never be reused across screens. This can cause issues when it comes to changing a string for a specific screen. It saves future complications by having a single string for each screens usage.

 - String resources should **always** be defined in the strings file and never hardcoded in layout or class files.


### Sectioning code

String resources defined within the strings.xml file should be section by feature, for example:

```xml
    // User Profile Activity
    <string name="button_save">Save</string>
    <string name="button_cancel">Cancel</string>

    // Settings Activity
    <string name="msg_instructions">...</string>
```

Not only does this help keep the strings file tidy, but it makes it easier to find strings when they need altering.

## styles.xml

### Styles and Themes Naming

When defining both Styles & Themes, they should be named using UpperCamelCase. For example:

```
    AppTheme.DarkBackground.NoActionBar
    AppTheme.LightBackground.TransparentStatusBar

    ProfileButtonStyle
    TitleTextStyle
```

## xml

# Best Practices

## Use self closing tags

When a View in an XML layout does not have any child views, self-closing tags should be used.

Do:

```xml
    <ImageView
        android:id="@+id/imageview_user"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />
```

Don’t:

```xml
    <ImageView
        android:id="@+id/imageview_user"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content">
    </ImageView>
```

## Remove unused resources

Unused resources and ids should be removed from the project.

Use **Refactor -> Remove Unused Resources** in menu bar to remove unused resources.
