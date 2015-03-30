# Saving Data

- One way is to use a really convenient key-value store called "Shared Preferences"
- A second way is to store onto a file
- A third way is to create your own SqlLite table (this is more involved).

## Shared Preferences 

1)  Make the following class members of your activity (when you are doing the editing especially)

```java
    private SharedPreferences shared_pref;
    private SharedPreferences.Editor editor;
```

2)  initialize sharedPref with your application's context

Place this in your onCreateMethod (after setting the content view)

**Note: Replace "keyval_name_here" with a name for your key-value storage.**

```java
shared_pref = getApplicationContext().getSharedPreferences(
                "keyval_name_here", Context.MODE_PRIVATE);
```

3) add or edit a key-value pair

```
  editor = shared_pref.edit();
  editor.putString("phone_number", "4445556666");
  editor.commit();
```

Similarly there is a `putInt` method for editor as well.


## Retrieving values from SharedPreferences Keystore


Simply enter the key of the int or String, and store the value appropriately:

**Note: Replace "keyval_name_here" with the name for your key-value storage.**

```java

SharedPreferences shared_pref = getApplicationContext().getSharedPreferences(
"keyval_name_here", Context.MODE_PRIVATE);
String default_val = "no phone number";
String phone_number = shared_pref.getString("phone_number", default_val);
```

If you would like, you can display this via a textview:

```java
TextView text_view = (TextView) findViewById(R.id.text_view);
text_view.setText(phone_number);
```

Tada!

===

## Saving to a File


#### Internal Storage

```Java
                // write something to do if clicked below
                String current_time = String.valueOf(System.currentTimeMillis());

                String filename = "my_first_data_file.csv";
                FileOutputStream outputStream;/
                try {
                    outputStream = getActivity().openFileOutput(filename, getActivity().MODE_PRIVATE);
                    outputStream.write(current_time.getBytes());
                    outputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
                Toast.makeText(getActivity(), "time, "+ current_time, Toast.LENGTH_SHORT).show();
```

#### External Storage


*Writing (appending) to an external file*

```java
Button bob = (Button) rootView.findViewById(R.id.button);
  bob.setOnClickListener(new View.OnClickListener() {
        public void onClick(View view) {
            File file = new File(getActivity().getExternalFilesDir(null), "test_storage.csv");

            String line ="time, "+ String.valueOf(System.currentTimeMillis() + "\n");
            try {
                OutputStream os = new FileOutputStream(file,true); // true so we can append
                os.write(line.getBytes()); 
                os.close();
            } catch (IOException e) {
                // Unable to create file, likely because external storage is
                // not currently mounted.
            }
        }
});
```


*Sending external file via email*

```java
Button rufus = (Button) rootView.findViewById(R.id.button2);
    rufus.setOnClickListener(new View.OnClickListener() {
        public void onClick(View view) {
            // write something to do if clicked below
            File file = new File(getActivity().getExternalFilesDir(null), "test_storage.csv");

            String emailAddress = "gregory.kielian@gmail.com";
            String subject = "App Send An Email";
            String message = "Sup. My app just send you an email whenever I press this button...";

            Uri U = Uri.fromFile(file);
            Intent intent = new Intent(Intent.ACTION_SEND);
            intent.setType("text/csv");
            intent.putExtra(Intent.EXTRA_STREAM, U);
            intent.putExtra(Intent.EXTRA_SUBJECT, subject);
            intent.putExtra(Intent.EXTRA_EMAIL, new String[] { emailAddress });
            intent.putExtra(Intent.EXTRA_TEXT, message);
    
            startActivity(Intent.createChooser(intent,"Email:"));
    }

});
```


## Saving to SQLLite database

TODO
