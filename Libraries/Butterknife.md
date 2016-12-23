# Butterknife

Butterknife is a library that provides field and method bindings using annotations to reduce the boilerplate code.

## Binding Views

Butterknife view bindings allow eliminations of findViewById by using the @BindView on fields.

### Activity Binding

Annotate fields with @BindView and a view ID for Butter Knife to find and automatically cast the corresponding view in your layout.

```java
class ExampleActivity extends Activity {

    @BindView(R.id.title)
    TextView title;

    @BindView(R.id.subtitle)
    TextView subtitle;

    @BindView(R.id.footer)
    TextView footer;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.simple_activity);
        ButterKnife.bind(this);
        // TODO Use fields...
    }
}
```

### Non-Activity Binding

You can also perform binding on arbitrary objects by supplying your own view root.

```java
public class FancyFragment extends Fragment {

    @BindView(R.id.button1)
    Button button1;

    @BindView(R.id.button2)
    Button button2;

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fancy_fragment, container, false);
        ButterKnife.bind(this, view);
        // TODO Use fields...
        return view;
    }
}
```

Another use is simplifying the view holder pattern inside of a list adapter.

```java
public class MyAdapter extends BaseAdapter {

    @Override
    public View getView(int position, View view, ViewGroup parent) {
        ViewHolder holder;
        if (view != null) {
          holder = (ViewHolder) view.getTag();
        } else {
          view = inflater.inflate(R.layout.whatever, parent, false);
          holder = new ViewHolder(view);
          view.setTag(holder);
        }

        holder.name.setText("John Doe");
        // etc...

        return view;
    }

    static class ViewHolder {

        @BindView(R.id.title)
        TextView name;

        @BindView(R.id.job_title)
        TextView jobTitle;

        public ViewHolder(View view) {
            ButterKnife.bind(this, view);
        }
    }
}
```

## Listener Bindings

Where possible, make use of Butterknife listener bindings.

### OnClick

When listening for a click event instead of doing this:

```java
    submitButton.setOnClickListener(new View.OnClickListener() {
        public void onClick(View v) {
            // Some code here...
        }
    });
```

do this:

```java
    @OnClick(R.id.button_submit)
    public void onSubmitButtonClick() { }
```

### OnEditorAction

For setting done action for an `EditText`, instead of doing this:

```java
    passwordEditText.setOnEditorActionListener(new TextView.OnEditorActionListener() {
        @Override
        public boolean onEditorAction(TextView v, int actionId, KeyEvent event) {
            if (actionId == EditorInfo.IME_ACTION_DONE) {
                login();
                return true;
            }
            return false;
        }
    });
```

do this:

```java
    @OnEditorAction({R.id.edittext_password})
    public boolean onPasswordEditTextDone(int actionId) {
        if (actionId == EditorInfo.IME_ACTION_DONE) {
            login();
            return true;
        }
        return false;
    }
```

## References
- http://jakewharton.github.io/butterknife/
- https://github.com/JakeWharton/butterknife
