## Make a splashscreen

In order to make a splashscreen you will need to do a few things:


1) make a blank activity 
2) change `extends ActionBarActivity` to `extends Activity`
3) go to res/styles

```
<style name="noTitleBar" parent="Theme.AppCompat.Light.NoActionBar">
        <!-- Customize your theme here. -->
        <item name="android:windowNoTitle">true</item>
        <item name="android:windowActionBar">false</item>
</style> 
```

4) go to AndroidManifest.xml and add the `android:theme="@android:style/Theme.NoTitleBar"`

```
<activity
             android:name=".SplashScreen"
             android:label="@string/title_activity_splash_screen"
             android:theme="@android:style/Theme.NoTitleBar">
```
