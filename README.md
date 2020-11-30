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
1. Go to mitm.it on your android device
2. download the certificate 
3. install it 
</br>
now you should be able to debug https to

#### 1.2.2 installing ca certifcate on android >= *Android Nougat*
