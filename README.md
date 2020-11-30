# hacking android apps
it's important to understand how the app works; at least at a basic level. 
otherwise you won't be able to find weak points.
## 1. debug http(s) requests
i like to analyse the requests that are send and receive from the app. sometimes there are more data than shown in the application.
you can use any rest-client to test after you analyzed to test or fake requests.
### 1.1 app has a web version
it makes this step easier because you can use the **development tools** of you browser. like the Chrome DevTools in the Chrome browser.
### 1.2 there is no web version 
it that case i use *mitmweb* from https://mitmproxy.org/ because it is free and open source. 
1. run *mitmweb* on you pc
2. find out you pc's ip adress on you local network
3. change the network settings of your android device <br/>
in the proxy setting you enter the ip adress of the pc and the port 8080
now the android device connects through your pc with the internet. <br/>

now on the pc with http://localhost:8081/ you can debug http requests. <br/>
**for https requests you need to install a certificate on your android device**
#### 1.2.1 installing ca certificate on android < *Android Nougat*
1. Go to website **mitm.it** on your android device
2. download the certificate 
3. install it 



#### 1.2.2 installing ca certifcate on android >= *Android Nougat*

1. Go to website **mitm.it** on your android device
2. download the certificate 
3. install it 

> Since Android 7, apps ignore user certificates, unless they are configured to use them. As most applications do not explicitly opt in to use user certificates, you need to place the mitmproxy CA certificate in the system certificate store, in order to avoid having to patch each application, which you want to monitor. 

now you should be able to debug https too

## 2. analysis of the coding

get the apk on the pc from the android device with an usb cable

0. Check connection with the android device via comand `adb devices` on the terminal
1. Determine the package name of the app, e.g. *"com.example.someapp"*. Skip this step if you already know the package name. </br>
`adb shell pm list packages` </br>
Look through the list of package names and try to find a match between the app in question and the package name. This is usually easy, but note that the package name can be completely unrelated to the app name. If you can't recognize the app from the list of package names, try finding the app in Google Play using a browser. The URL for an app in Google Play contains the package name.
2. Get the full path name of the APK file for the desired package. </br>
`adb shell pm path com.example.someapp` </br>
The output will look something like </br>
*pckage:/data/app/com.example.someapp-2.apk* </br>
or </br>
*package:/data/app/com.example.someapp-nfFSVxn_CTafgra3Fr_rXQ==/base.apk*
3. Using the full path name from Step 2, pull the APK file from the Android device to the pc </br>
`adb pull /data/app/com.example.someapp-2.apk path/to/desired/destination`

get the coding from the apk. i am using JADX https://github.com/skylot/jadx but there are other tools also. just google. 
