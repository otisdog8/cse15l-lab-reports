# How to remotely access ieng6

## Step 1: Installing VSCode
I already had vscode installed, so I didn't need to install it. If I wanted to install vscode, I would start with installing an [AUR](https://wiki.archlinux.org/title/Arch_User_Repository) helper, yay. I would do this by running the following commands in a terminal:
```bash
cd /tmp
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```
Then, I would install vscode by running the following command
```bash
yay -S visual-studio-code-bin
```
Now, I can open vscode:
![](https://media.discordapp.net/attachments/527258492286009344/1063217775436365864/image.png)
## Step 2: Remotely Connecting
I prefer the kitty terminal over the vscode integrated terminal, and it has special syntax for ssh that makes it's cursor render corrrectly, so I use this command to connect:
```bash
kitty +kitten ssh cs15lwi23aje@ieng6.ucsd.edu
```
You would do this without the kitty +kitten, and with a different username.
```bash
ssh $YOURUSERNAME@ieng6.ucsd.edu
```
This makes my cursor look like this:  

![](https://media.discordapp.net/attachments/527258492286009344/1063236242143182949/image.png)  

as opposed to this (without using kitty +kitten):  

![](https://media.discordapp.net/attachments/527258492286009344/1063236488508215407/image.png)  

After that, you should say yes to this prompt (it might look different on your computer):  

![](https://media.discordapp.net/attachments/527258492286009344/1063237385279778886/image.png)  

Then, you should enter your password (it might look different on your computer):  

![](https://media.discordapp.net/attachments/527258492286009344/1063237983651762206/image.png)  

Now, I'm in, and the prompt looks like this:  

![](https://media.discordapp.net/attachments/527258492286009344/1063238187301994506/image.png)  

## Step 3: Trying Some Commands
