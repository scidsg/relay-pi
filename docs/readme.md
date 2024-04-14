# Installing Pi Relay

## Raspberry Pi Prerequisites

### Hardware

- **Hardware:** [Raspberry Pi 4](https://www.amazon.com/Raspberry-Model-2019-Quad-Bluetooth/dp/B07TC2BK1X/?&_encoding=UTF8&tag=scidsg-20&linkCode=ur2&linkId=ee402e41cd98b8767ed54b1531ed1666&camp=1789&creative=9325)/[3B+](https://www.amazon.com/ELEMENT-Element14-Raspberry-Pi-Motherboard/dp/B07P4LSDYV/?&_encoding=UTF8&tag=scidsg-20&linkCode=ur2&linkId=d76c1db453c42244fe465c9c56601303&camp=1789&creative=9325)
- **Power:** [Raspberry Pi USB-C Power Supply](https://www.amazon.com/Raspberry-Pi-USB-C-Power-Supply/dp/B07W8XHMJZ?crid=20ZD3IB2N877C&keywords=raspberry%2Bpi%2Bpower%2Bsupply&qid=1696270477&sprefix=raspberry%2Bpi%2Bpower%2B%2Caps%2C140&sr=8-5&th=1&linkCode=ll1&tag=scidsg-20&linkId=fa55eb4c089361952be8285bf67bfd22&language=en_US&ref_=as_li_ss_tl)
- **Storage:** [Micro SD Card](https://www.amazon.com/Sandisk-Ultra-Micro-UHS-I-Adapter/dp/B073K14CVB?crid=1XCUWSKV8V2L1&keywords=microSD+card&qid=1696270565&sprefix=microsd+car%2Caps%2C137&sr=8-21&linkCode=ll1&tag=scidsg-20&linkId=a2865a28ae852876a5a6d27512e9d7ef&language=en_US&ref_=as_li_ss_tl)
- **SD Card Adapter:** [SD Card Reader](https://www.amazon.com/SanDisk-MobileMate-microSD-Card-Reader/dp/B07G5JV2B5?crid=3ESM9TOJBH8J7&keywords=microsd+card+adaptor+usb+sandisk&qid=1696270641&sprefix=microsd+card+adaptor+usb+sandisk%2Caps%2C135&sr=8-3&linkCode=ll1&tag=scidsg-20&linkId=90d3bed4e490d29d84bcf86d9fe75290&language=en_US&ref_=as_li_ss_tl)
- _Affiliate links_

### Prepping Your Pi

If you didn't know, your Raspberry Pi doesn't come with an operating system. Don't panic! We're going to install one now called Raspberry Pi OS.

#### 1. Raspberry Pi Imager

Like a Macbook runs MacOS, and a Dell runs Windows, a Raspberry Pi runs Linux, which comes in many different flavors depending on your needs. Since we're using a Raspberry Pi, we'll use Raspberry Pi OS (64-bit), an operating system made just for the Pi. The Imager installs the operating system onto your microSD card, where we'll set up Hush Line. Download it from https://www.raspberrypi.com/software/.

<img src="../img/1-rpi-imager.png">
<img src="../img/2-rpi-imager.png">

### Prep Your Card

#### 2. Install Raspberry Pi OS
Open the Raspberry Pi Imager and click `Choose OS > Raspberry Pi OS (other) > Raspberry Pi OS (64-Bit)`.

Insert your microSD card into your computer, and then click `Choose Storage` and select your card.

<img src="../img/19-rpi-imager.png">

Before clicking Write, click on the Settings gear in the bottom right of the window. Configure the following settings:

- Hostname = `pirelay`
- Enable SSH with password authentication
- User = `operator`
- Set a strong password
- Add wifi settings

<img src="../img/20-advanced.png">

### Boot up and log in to Your Pi

#### 3. Insert microSD Card

Take your SD card and insert it into your Raspberry Pi. You'll find the SD card slide on the bottom of the board, opposite the ethernet ports.

Plug the power supply into the device and let it boot up.

#### 4. Log In

On a Mac, open Spotlight search by pressing CMD + Space. Enter "Terminal" and select the application with the same name.

Enter `ssh operator@pirelay.local`, and when prompted, enter the password you created in the second step.

<img src="../img/21-terminal-login.png">

#### 5. Update your system

The last thing we need to do is to update our system. First, we'll give ourselves admin priviledges, then perform the update:

Enter `sudo su`, then `apt update && apt -y dist-upgrade && apt -y autoremove`.

<img src="../img/21-update.png">

🎉 That's it, you're ready to get started with Raspberry Pi!

Pi Relay is made for Raspberry Pi and uses an e-paper display to show real-time information about your relay's activity.

To start the installer, enter:

`curl --proto '=https' --tlsv1.2 -sSfL https://install.pirelay.computer | bash`

### Choose Your Relay Type

After the install script begins, you'll choose the kind of relay you want to configure. Making the right decision for your installation environment will be necessary.

#### Types of Relays

After the install script begins, you'll choose the kind of relay you want to configure. Making the right decision for your installation environment will be necessary.

##### How Tor Works

First, let's understand how Tor works before choosing the kind of relay to use. [Tor](https://torproject.org) offers online anonymity by hiding information about your digital footprint, including your IP address, browser size, and operating system.

Think back to your preschool days when you wanted to send a secret "I <3 U" note to a crush. You asked your bestie to deliver it, ensuring your crush remained clueless about the admirer. In this analogy, your friend acts as a relay for you. But instead of the note going from you to your bestie to your crush, it goes from you to three random volunteers around the world, who you don't know but will deliver the message.

##### Entry Relays

In your chain of three volunteers delivering your note, the first person is the entry relay. The Tor network itself chooses relays based on factors including stability and performance. The entry doesn't know the destination address.

##### Middle Relays

A middle relay is the second person in the chain. They don't know who you are, and they don't know who your crush is - they're simply a middle-person.

⭐️ If you operate a relay from home, you should only choose a middle relay.

##### Exit Relays

Exit relays are the last step in the chain, and will request the website on your behalf. They don't know who you are but know who your crush is. Operating an exit relay should take extra consideration and should _never_ be operated from home.

Here's a real example of why you shouldn't operate an exit from home: back in 2019, [Trump's Justice Department demanded 1.3 million IP addresses of the people who visited a Trump protest website](https://arstechnica.com/tech-policy/2017/08/feds-demand-1-3-million-ip-addresses-of-those-who-visited-trump-protest-site/). Why did they want the IP addresses? What if you never visited the site, but it looked like you did? Could you potentially get in trouble?

If you run an exit relay, it will appear that _YOUR_ IP address is the one visiting the site.

So if the teacher catches you handing the note, it will look like it's from you.

Again, never operate an exit relay from home. Businesses and public institutions like libraries and universities - who can donate high-speed internet and have enough money to afford legal council if needed - should only consider this option.

##### Bridge Relays

Bridge relays are a special type of relay. Sometimes, the Tor Network can be blocked completely. When this happens, bridge relays are the ones who become the entry. You can share your bridge address for someone to plug into Tor Browser, or Tor can share it automatically for you.

This person is the silent helper who will step in if all else goes wrong. They'll ensure the note is discretely delivered.

For this guide, we'll choose a middle relay.

###### Configure Relay Information

You need to set a few variables before your relay can go online.

###### Relay Nickname

We automatically generate a nickname that looks like `pirelay231009`. Avoid using special characters, spaces, or long names if you change it.

###### Port

Your relay needs a port to make itself available to pass information. You must also forward this port if you're running the relay from home. If you don't know how, search for your router's instructions. 

We pre-fill this option with port 443, the port used for secure HTTPS web requests. The default port that Tor uses is 9001, but this can be easily blocked. To get around port censoring, we chose 443 because blocking this would mean blocking much of the internet.

###### Monthly Bandwidth Quota

This is your "accounting max". To make it easy, we set this up as a monthly quota. Middle relays are required to share a minimum of 200 GB per month.

###### Bandwidth Limits

You'll set your bandwidth limit and burst rates. Tor recommends at least 2 MB/s, with a 4 MB/s burst. These values are entered by default for you.

###### Contact Info

You can optionally add your name and email address so Tor can notify you if your relay ever goes down. There's a default value entered for you, but consider adding an address you have access to.

## Using Pi Relay

Once Pi Relay is running, you don't have to do anything! Since you have an e-paper display, you can check in on its activity to see how much bandwidth you've donated.

### Automatic Updates

One of the tricky things about operating a relay is keeping it up-to-date. We handle this for you by automatically updating your device. You'll be able to see the Tor version on the diaplay to confirm it's working.

### Flags

At first, you'll notice "No flags yet." After it's running for some time flags like "Running," "Valid," "Stable," or "Fast" will begin to display.

### Bar Chart

You'll see a bar chart visualizing your bandwidth contributions relative to your monthly quota. Your display refreshes every minute, so you always know your most recent activity.
