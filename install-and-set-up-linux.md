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
