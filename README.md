## Sing_in_with_Facebook_flutter_right_way


## Flutter Google and Facebook Authentication


google authentication with firebase
Google authentication without firebase
facebook auth


## Authentication using google 

1.Authentication using google with firebase
Requirement:
a)create a new flutter project.
  Add these packages in pubspec yaml file :
  1.firebase core
  2.firebase auth
  3.google sign

b)open your firebase console account.Add your project in firebase with package name and SHA1 key.
Where do you get the project package name?
Folder : android>app>src>main>res>AndroidManifest

How to create a SHA1 key?
Command : 
keytool -list -v -keystore ~/.android/debug.keystore -alias android_debugkey -storepass android -keypass android

source : https://stackoverflow.com/questions/30070264/get-sha1-fingerprint-certificate-in-android-studio-for-google-maps


c)Add all the firebase dependencies in your project following the instruction of firebase.

d)Download the service json file and add in your project app folder.

e)Build a login screen ui with a login button.
f)Write a function for handling user login and logout. Call the function in the onPressed  method of your login button.

For Login, 
Example:

	signInWithGoogle() async {
    try {
      final GoogleSignInAccount? googleSignInAccount =
      await _googleSignIn.signIn();
      if (googleSignInAccount != null) {
        final GoogleSignInAuthentication googleSignInAuthentication =
        await googleSignInAccount.authentication;
        final AuthCredential authCredential = GoogleAuthProvider.credential(
            accessToken: googleSignInAuthentication.accessToken,
            idToken: googleSignInAuthentication.idToken);
        await _auth.signInWithCredential(authCredential);
      }
    } on FirebaseAuthException catch (e) {
      print(e.message);
      throw e;
    }
  }







For Logout, 
Example:

googleSignOut() async {
    await _auth.signOut();
    await _googleSignIn.signOut();
  }

Before Run your project : 
 	Make changes in 
		        compileSdkVersion 31
		        minSdkVersion 22
        		        targetSdkVersion 31

Then in Android Studio : 

File>Project structure>select diversion android 31>click on problems>again select SDK version then apply all changes and save.Hopefully you can overcome the firebase gradle-build error by doing this.

Also If you face in generating keystone files then go to the environment variable and add your java jdk/jre path properly.

Finally execute your project.


 2.Authentication using google without firebase

Requirement:

a)create a new flutter project.
  Add package :
  	google sign

2.Open your google cloud console account.Add your project in cloud console with project package name and SHA1 key(generate same way as previously said).

3.Generate a keystore file from the terminal by using this command :

  keytool -list -v -keystore ~/.android/debug.keystore -alias android_debugkey       -storepass android -keypass android

more about this command : https://stackoverflow.com/questions/30070264/get-sha1-fingerprint-certificate-in-android-studio-for-google-maps

Keep notes:
*your alias name
*your key store .jks file name and path
*password of key store file
Add this information in your build gradle-build file.
 Example : 

  signingConfigs {
        debug {
            keyAlias 'upload'
            keyPassword '12345678'
            storeFile file('upload-keystore.jks')
            storePassword '12345678'
        }
    }








Write a login function look like this and call the function from its onPressed method: 

 GoogleSignIn _googleSignIn = GoogleSignIn();
    try {
      var result = await _googleSignIn.signIn();
      if(result!=null){
      print(result);
    } catch (error) {
      print(error);
    }
  }


Before Run your project : 
 	Make changes in 
		        compileSdkVersion 31
		        minSdkVersion 22
        		        targetSdkVersion 31

Then in Android Studio : 

File>Project structure>select diversion android 31>click on problems>again select SDK version then apply all changes and save.Hopefully you can overcome the firebase gradle-build error by doing this.

Also If you face in generating keystone files then go to the environment variable and add your java jdk/jre path properly.

Finally execute your project.


 3.Authentication using Facebook

Requirement:

1.Create a new flutter project
	add packages :
	flutter_facebook_auth: ^5.0.6

2.Create an account on developer Facebook.
	add your application
	follow the instructions and add all the necessary dependencies in your     application.





Problem you might Face with Facebook login :

error in manifest file

Possible Solution for your problem :

Add these lines after the package name in the manifest file.

<provider android:authorities=“com.facebook.katana.provider.PlatformProvider” />
</queries>

