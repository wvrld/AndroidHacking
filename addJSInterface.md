# AddJavascriptInterface

    The Webview addJavaScriptInterface exploit is one of the most interesting
    remote exploits that has been discovered so far, but they wont probably work on new devices.

    This vulnerability exploits the fact
    that the Java reflection APIs are publicly exposed via the WebView
    JavaScript bridge.

    Although we are going to use the Metasploit framework in this
    section to trick the user into opening a link in a vulnerable browser, this exploit can
    also be used with a MiTM attack, tricking a vulnerable application to execute
    malicious JavaScript injected into its response. Applications that are targeting API
    levels <=16 are vulnerable.

# Launch Metasploit's msfconsole and search for `webview_addjavascript`

<img src="https://media.discordapp.net/attachments/842658705489264650/878016851773366283/unknown.png"/>

    As we can see, we got two different modules in the output.
    `exploit/android/browser/webview_addjavascriptinterface` is the one we are looking for.
    So, Lets use it!

<img src="https://media.discordapp.net/attachments/842658705489264650/878018139571511296/unknown.png"/>

    We loaded the module so lets setup the options using `show options`

<img src="https://media.discordapp.net/attachments/842658705489264650/878018510754816000/unknown.png"/>

    As you can see, LHOST is the only entry missing in the payload section.
    So, lets find our IP adress using the `ifconfig` command.

<img src="https://media.discordapp.net/attachments/842658705489264650/878019085588377610/unknown.png"/>

    In my case, its 10.0.0.6. Lets set the LHOST with this IP Address.

<img src="https://media.discordapp.net/attachments/842658705489264650/878019474580705321/unknown.png"/>

    We have everything ready, now lets run the exploit by typing `exploit`

<img src="https://media.discordapp.net/attachments/842658705489264650/878019850402926642/unknown.png"/>

    As you can see, a reverse handler is running on port `4444`. 
    Now, we can pass the link `http://0.0.0.0:8080/olcbdc3Nj2E1` to the victim.

    When the victim opens the link in vulnerable browser, it gives a reverse shell to the attacker. Sadly, i dont have any android device on me right now so i cant show you how it looks on attacker side.

# Note 

    We can execute this attack remotely without user intervention if we use any of
    the traditional MitM attacks. The idea is to perform MitM and inject malicious
    JavaScript into the http response and execute it to through the Java Reflection APIs
    exposed via the WebView JavaScript interface. But it will works only when apps are targeting API levels <= 16. 

Next Part - Bypassing ScreenLocks and Pulling data from SD card.
