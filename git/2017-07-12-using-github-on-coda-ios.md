# GitHub on Coda iOS
> :calendar: *July 12, 2017*

Coda on iOS is a great little text editor, but it lacks GitHub integration. I've found two approaches to getting it to work.

### The GUI Way
The easiest way to edit GitHub repos using Coda is to also purchase Working Copy. You can try Working Copy for free, but you'll have to pay $15 to unlock push capability.

1. Clone the repo in Working Copy.
2. Go to settings, enable the WebDAV server, and set the host name to `localhost` (read more [here](https://workingcopyapp.com/manual/extending-ios)).
3. In Coda, create a new site or edit an existing site.
4. Under the Remote tab (the globe icon), select WebDAV under server and use the information from Working Copy.

Inside your site (Coda's name for a project), you should now have a local tab and remote tab. You can edit the files in the remote tab, and when you're ready to commit and push, switch back to Working Copy. In order to use Coda's live preview, you do need to have a local copy of the `index.html` and any necessary assets.

### The CLI Way
This is my method of choice, since you'll be able to take advantage of Coda's terminal emulator and actually have access to a Linux VM so you can work on Express apps or use Webpack to compile and bundle your JavaScript.

1. Set up a Linux VM. Google Cloud gives you a free Compute Engine instance, which is what I'm using.
2. In Coda, Create a new site or edit an existing one. Under the Terminal tab, click the key icon. Click the + (plus) button to generate a new key. Select RSA 2048 and give it a nickname (you can name it the name of your Google Cloud ProjectID). When it's finished, click "copy public key".
3. In your mobile browser, log into your Google Cloud Platform account and open the project with your Compute Engine instance.
4. Click the Compute Engine navigation link, and then click Metadata.
5. On the Metadata page, click SSH Keys.
6. Click Edit then click Add Item.
7. Paste the Public Key you copied from Coda. Make sure to start it with `ssh-rsa` and end it with the name you want to log into your server with. For example: `ssh-rsa <key> adam` (read more [here](https://cloud.google.com/compute/docs/instances/connecting-to-instance))
8. Under the VM Instances navigation link, click the external IP address. It will open a browser window. Copy the IP address from the address bar (you don't need the HTTPS:// at the front).
9. Back in Coda, paste the IP Address in the SSH Address field, enter the username you added to the Compute Engine Metadata, and select the key you previously generated.
10. In Coda, under the Remote tab (the globe icon), select SFTP and paste the IP Address in the Address field, enter your username again, and select the key again.
11. You can set Remote Path to `/home/username` or whatever root folder you want to store your projects in. Remote URL won't do anything if you're not running a web server.

You'll now be able to SSH into your VM and use Git like you normally would. Once you've cloned or pulled the repository you want to work on, you can simply edit the files you want under the Remote tab in Coda. When you're ready to commit your changes, just go back to the Terminal.

Note that since you're using a fresh operating system, so you'll want to set up your `.gitconfig` (name and email at a minimum) and optionally install [hub](https://hub.github.com). Ubuntu comes with Git installed, but you also may want to upgrade it. You'll also need to install Node/NVM and any global NPM packages that you use regularly (like gh-pages).

The benefit of setting up Coda like this is that you now have access to a fully-functional Linux computer where you can install Node, use Webpack or Create React App, or even set up an Express server on port 80 to host whatever you're working on.

You will need to copy any files over locally if you want to use Coda's live preview (i.e., just your `index.html` and `bundle.js` and any other assets).
