# Install Ubuntu Linux desktop

## Hardware
Make sure hardware is compatible, I almost bought the wrong stuff.

Box is Asus PN51 (lucky chance, had been on waitlist for a PN50 for months when this suddenly appeared as available).

Reddit thread about memory for this box: https://www.reddit.com/r/MiniPCs/comments/jwvp60/endless_problems_with_asus_pn50/

I got the HyperX Impact DDR4 3200MHz - 2x16GB CL20

For storage I got the Samsung 970 EVO Plus 500GB SSD as it should be recognized by the BIOS as-is. 1TB variant and other makes, formatted to 16k blocks instead of 4k like the 970 500GB was supposedly not recognized and so nothing could be installed. Can't find source for that right now, will add later

## Installing Ubuntu
It is possible to create a boot device that will let you try Ubuntu on your hardware before actually installing it. This can also be used to actually install Ubuntu. Guide below.

### Preparing the boot device
Having an existing Windows 10 system to create the installation media, the Ubuntu guide was easy and straight forward to follow:
https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview

In short:
1. Download the Ubuntu Desktop ISO file from here: https://ubuntu.com/download/desktop
I got the just released 21.04 version as it has better AMD Ryzen support, which is what the Asus PN51 has
2. Download Rufus, a program that can write ISO images to an USB stick
3. Launch Rufus
4. Insert the USB stick that will be formatted, so make sure it is empty first, and select it as the device in Rufus if it wasn't automatically
5. Set boot selection to FreeDOS if it isn't already
6. Click the select button, and select the Ubunto ISO image that was downloaded
7. Click the start button to start the writing process
8. There will be a warning since it is a hybrid image that can be used both for DVD and USB, make sure ISO image is selected and continue

### Installing or trying Ubuntu
When booting, select "Try Ubuntu" to see what Ubunto Desktop is and if it works with your hardware without actually installing it, or "Install Ubuntu" to install it.

Follow the installation guide:
https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview

Tutorial was easy and straight forward so didn't think to write down what I did, but the guide covers the options.

# Add multimedia codecs
It turns out multimedia playback doesn't work perfectly in browsers on Linux by default, as some multimedia codecs are not installed.

The multimedia codecs are called "ubuntu-restricted-extras" and can be installed from commandline or the Ubuntu software store following this guide: https://www.ubuntupit.com/how-to-install-multimedia-codecs-on-ubuntu-linux/

In short, using the Ubuntu software store:
1. Copy and paste this link into a browser: ```apt:ubuntu-restricted-extras?section=universe?section=multiverse```
2. Select to open the link in Ubuntu software
3. Click install

# Install a new terminal
I like the terminal called Hyper as it can be used on all of Windows, Mac and Linux, so you can have the same setup if you use different systems.

Page: hyper.is

1. Go to "Installation" and download the Debian (.deb) file. The .AppImage might be more portable, but it starts up a lot slower, and I have experienced some problems with it I don't get with the .deb file.
2. Open the file from the browser, and select to open it with Ubuntu software
3. Click install

When hyper is launched, right click on the icon in the favorites bar to the right and select "Add to favorites" to keep it easily accessible.

# Install a new shell - zsh
From the commandline:

```zsh
$ sudo apt install zsh
```

Set zsh as the default shell for the logged in user:

```zsh
$ chsh -s /usr/bin/zsh
```
# Install oh my zsh
For managing your zsh configuration with themes and plugins that help with usability and productivity.

Page: https://ohmyz.sh/

Get the install script:
```zsh
$ curl -o install-oh-my-zsh.zsh -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh
```
It is wise to inspect it and see that it doesn't do anything malicious.

Run it to activate oh my zsh:
```zsh
$ sh ./install-oh-my-zsh.sh
```
# Install zsh auto-suggestions
_[Fish](https://fishshell.com/)-like fast/unobtrusive autosuggestions for zsh._

It suggests commands as you type based on history and completions. As you type commands, you will see a completion offered after the cursor in a muted gray color.

To install, clone the repository into the custom plugins folder for oh-my-zsh. On the command line:
```zsh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

To activate it, add it to the list of plugins oh-my-zsh will load. In `~/.zshrc` find the `plugins=` line and add it. If only the git plugin was activated before, it should look like this:
```zsh
plugins=(git zsh-autosuggestions)
```

Now restart the shell.

# Download and install powerline fonts
According to the documentation, "powerline is a statusline plugin for vim, and provides statuslines and prompts for several other applications." The powerline fonts are patched for powerline, and are used to easily see wanted status: Of current working directory, current git branch, number of git changes since last push and many other things.

For a general collection of powerline fonts: https://github.com/powerline/fonts but many other can be found online. https://www.nerdfonts.com/ is another notable page.

I'm using Fira Code which can be installed with apt:

```zsh
$ sudo apt install fonts-firacode
```
Then tell the terminal (Hyper) to use it, by adding it first to the font family configuration. Hyper configiration can be opened by pressing ```ctrl comma``` at the same time when in the terminal, or open the file ```~/.hyper.js``` in your favorite editor. The font config should look like this:
```zsh
fontFamily: '"Fira Code", Menlo, "DejaVu Sans Mono", Consolas, "Lucida Console", monospace',
```
To use the same font in VS Code, it has to be added there as well. Go to settings, which again can be opened with ```ctrl comma``` in the editor, then add it first on the font family config so it looks like this:
```zsh
'Fira Code', 'Droid Sans Mono', 'monospace', monospace, 'Droid Sans Fallback'
```
# Alternative fonts
There are many alternatives to select from, and I've recently switched to [Intel One Mono](https://github.com/intel/intel-one-mono). To install, download the `otf` version from `releases` and unzip it. Then double-click each font file in your choice of file explorer and you should get the option to install that font file. To use the new font, follow the same instructions as for `Fira Code` above. On Linux the font should be used like this: `'Intel One Mono'` while on Mac it seems to be installed as `'IntelOne Mono'`.

Another thing on Linux is that it might be necessary to install `font-manager` if it doesn't come with the distribution: `sudo apt install font-manager`

I've switched to a zsh-shell theme called `powerlevel10k` and they recommend using a font called [MesloLGS NF](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k) and they have their own patched version of it with all the symbols needed for their themes, but I find Intel One works just as well. If there are issues with symbols when configuring (like lock and arrow up symbol not showing) you will actually have to have the MesloLGS NF font installed and in your terminals font path, but I've not experienced any other issues other than when configuring.


# Download and install the cobalt2 theme
One of the points of using oh-my-zsh for me is that it supports themes. It does come with a lot of them you can experiment with, but I'm using Cobalt2 by [Wes Bos](https://wesbos.com/).
Cobalt2 can be found here: https://github.com/wesbos/Cobalt2-iterm

Go to the custom themes directory for oh-my-zsh which is in ```~/.oh-my-zsh/custom/themes```

Clone the cobalt2 repository:
```zsh
$ git clone git@github.com:wesbos/Cobalt2-iterm.git
```

Symlink the zsh-theme to cobalt2.zsh-theme in the current directory:
```zsh
$ ln -s Cobalt2-iterm/cobalt2.zsh-theme cobalt2.zsh-theme
```
Then finally to make use of all we've done above, tell oh-my-zsh to use this theme by setting it in the ~/.zshrc file. The line to change is ```ZSH_THEME``` and it should be changed to ```cobalt2``` instead of ```robbyrussell``` which was the default when I wrote this.

Now you can easily see your working directory, what git branch is checked out, if working tree is clean or if there are uncomitted changes, and so on.

# Download and install Powerlevel10k
[Powerlevel10k](https://github.com/romkatv/powerlevel10k) is a theme for Zsh. It emphasizes [speed](https://github.com/romkatv/powerlevel10k#uncompromising-performance), [flexibility](https://github.com/romkatv/powerlevel10k#extremely-customizable) and [out-of-the-box experience](https://github.com/romkatv/powerlevel10k#configuration-wizard). There are many ways to install and use it, including stand-alone in case you don't want oh-my-zsh. I'll be using it with oh-my-zsh:

```zsh
$ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
Then set ZSH_THEME="powerlevel10k/powerlevel10k" in ~/.zshrc, replacing the "cobalt2" line if that was set. Now when you restart your shell the Powerlevel10k configuration wizard will start asking you quite a few questions how you want it configured. If it doesn't start automatically or if you want to re-run it, do so with: `p10k configure`. The configuration will be written to `~/.p10k.zsh`.


# Install Node.js
There are at least 3 ways to install Node:
1. Download and install directly from nodejs.org
2. Using apt to install either from Ubuntu official package or through a PPA (Personal Package Archive)
3. Install using nvm (Node Version Manager)

Tutorial on digital ocean: https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04

Option 1 seems to require a manual install which I didn't want to do. Could be there are some other ways, but I didn't spend much time investigating.

Option 2, through Ubuntu official package, seems to give you a potentially very old Node version that isn't updated. Ubuntu 20.04 seems to still install Node 10, so I didn't want to do that.

Option 2 but using PPA is something I'm not familiar with, so I didn't try that. Though the advantages of using apt and having a Node version installed globally is that any Node modules you install globally will be kept when you upgrade Node.
The disadvantage is that you can't easily install a new version to check it out, and then quickly switch back if you don't want to use it yet.

Option 3 is what I went for, as it allows you to have multiple Node versions installed at the same time, and quickly switching between them. The disadvantage to this approach however, is that any global Node modules installed really are local to the Node version being used at the time. Meaning, if you switch Node version, you have to install the global Node modules again. Fortunately there is a way to easily upgrade modules from one version to another with nvm.

Source for nvm is at https://github.com/nvm-sh/nvm

Download the install script, and as always inspect it and check that it won't be doing anything malicious:
```zsh
$ curl -o install-nvm.sh -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh
```
Then run it:
```zsh
$ bash ./install-nvm.sh
```
If you're using a different shell from bash, like zsh, the following will have to be added to your shells configuration. For zsh, it's ```~/.zshrc```:
```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
Restart your shell and nvm should be available.

Now to install a Node version, list available versions with long term support (lts):
```zsh
$ nvm ls-remote --lts
```
Then install the version you want, for instance v14.17.0. You don't need the v in front of version number:
```zsh
$ nvm install 14.17.0
```
Node should now be installed, and you can check the version with:
```zsh
$ node --version
```
