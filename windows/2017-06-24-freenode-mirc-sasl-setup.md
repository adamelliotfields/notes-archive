# Freenode mIRC SASL Setup
> :calendar: *June 24, 2017*

I had been using Textual on macOS which has SASL built-in. On Windows, mIRC requires a tiny bit of configuration.  

### Nickserv Registration
Follow the guide on [Freenode](https://freenode.net/kb/answer/registration).

### mIRC Options
1. Click the hammer icon next to the connect (lightning bolt) icon.
2. Under "Connect", add your nickname.
3. Under "Servers", find the "Freenode" folder, double-click "Random server".

### Download the SASL Script
[Download](https://raw.githubusercontent.com/freenode/www/master/sasl/sasl.mrc) from Freenode's GitHub repo and save in your mIRC scripts folder: `C:\Users\Adam\AppData\Roaming\mIRC\scripts`

### Add the Script to mIRC
1. Under "Tools", click "Scripts Editor".
2. Under the "Remote" tab, go to "File > Load" and select `sasl.mrc`.
3. Click "Yes" when the warning pops up.
4. Click "OK" to exit the script editor.

### Configure SASL
1. Under "Commands" click "mSASL v1.0 Beta [sans DLL]".
2. Click "Add Entry".
3. Fill in the following information:
   * Network: Freenode
   * Username: {your nickname}
   * NS Password: {your registered Nickserv password}
   * Domain: 0
   * Real Name: {your name}
   * Timeout: 30
   * AuthType: PLAIN
4. Click "OK" to save the network configuration.
5. Click "OK" to exit the SASL Manager.

### Connect to Freenode
Click the lightning bolt icon and after connecting you should see the following text in your Status window:

```
You are now logged in as Fieldsy.
-
SASL authentication successful
```
