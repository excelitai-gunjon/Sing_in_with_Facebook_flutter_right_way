# Sing_in_with_Facebook_flutter_right_way

Read my article in medium : 
https://medium.com/@bayazid.excelitai/flutter-facebook-authentication-c6a1cb8fa3a


Users can register in your application through their facebook account and it's really very easy to implement.

This article will demonstrate how to set up the Flutter app to implement Facebook Authentication.



## Follow the steps :

## Open your developer facebook console with your facebook account.

click here : https://developers.facebook.com

## 2. Click on create app.
Select Business Type then add your project name.

## 3. Choose your platform and click next.

## 4. Add this dependency in your app level gradle-build file and click next.

implementation 'com.facebook.android:facebook-android-sdk:latest.release'

## 5. Now you have to provide your package name in first textbox
 and Second one your_package_name.MainActivity

## 6. Generate a hash key using this command 

For Mac :
keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64

For Windows : 
keytool -exportcert -alias YOUR_RELEASE_KEY_ALIAS -keystore YOUR_RELEASE_KEY_PATH | openssl sha1 -binary | openssl base64

## 7. Open your project folder
android\app\src\main\res\values

add a file name as strings.xml and add these code inside the file.

<?xml version="1.0" encoding="utf-8"?>
<resources>
<string name="facebook_app_id">465379152419170</string>
<string name="fb_login_protocol_scheme">fb465379152419170</string>
<string name="facebook_client_token">465379152419170</string>
</resources>

Copy your facebook id from developer console account and paste above.


## 8. In your Android manifest file add these line before <application>

<queries>
 <provider android:authorities="com.facebook.katana.provider.PlatformProvider" />
 </queries>
<uses-permission android:name="android.permission.INTERNET" />


  <meta-data android:name="com.facebook.sdk.ApplicationId" android:value="@string/facebook_app_id"/>

 <meta-data android:name="com.facebook.sdk.ClientToken" android:value="@string/facebook_client_token"/>


  <activity android:name="com.facebook.FacebookActivity"
        android:configChanges=
                "keyboard|keyboardHidden|screenLayout|screenSize|orientation"
        android:label="@string/app_name" />
    <activity
        android:name="com.facebook.CustomTabActivity"
        android:exported="true">
        <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="@string/fb_login_protocol_scheme" />
        </intent-filter>
    </activity>



## 9. Create a new flutter project.

## 10. Add this package
 flutter facebook auth : https://pub.dev/packages/flutter_facebook_auth

## 11. Create a button named as Sign in with facebook in your login_screen file. Then call the sign in function from its onPressed method.

## Sign in function :

Future<void> _login() async {
 final LoginResult result = await FacebookAuth.instance
 .login();
if (result.status == LoginStatus.success) {
 _accessToken = result.accessToken;
 _printCredentials();
final userData = await FacebookAuth.instance.getUserData();
 // final userData = await FacebookAuth.instance.getUserData(fields: "email,birthday,friends,gender,link");
 _userData = userData;
 } else {
 print(result.status);
 print(result.message);
 }
setState(() {
 _checking = false;
 });
 }
 
## Sign out Function :

Future<void> _logOut() async {
 await FacebookAuth.instance.logOut();
 _accessToken = null;
 _userData = null;
 setState(() {});
 }


These are the most important settings you need to do before run your project.
