  Command line WPA

Sometimes you'll be at a command line with no access to GUI networking tools -- but your access point is secured with WPA. What do you do?

Assuming your wireless card actually works (i.e. iwconfig can see it and interact with it), using wpa_supplicant is actually pretty simple. Installing wpa_supplicant

Most distros nowadays have wpa_supplicant installed by default. If you have the commands wpa_passphrase and wpa_supplicant available, then you're good to go. Otherwise, you will need to install the package by doing something like (for Ubuntu):

$ sudo apt-get install wpasupplicant

Generating the config file

Now that wpa_supplicant is installed, we will create its configuration file. Once you know the SSID and WPA passphrase, all you have to do is run:

$ wpa_passphrase myrouter mypassphrase > wpa.conf
Of course, replace "myrouter" with the SSID of your router, "mypassphrase" with your WPA passphrase, and "wpa.conf" with whatever file you want to store the configuration in. This filename does not have to follow a particular format or have a particular extension.

Alternatively, to avoid typing the passphrase on the command line (so it doesn't get saved in the shell's history), you can specify just the SSID on the command line. wpa_passphrase will wait for you to type in the passphrase followed by enter:

$ wpa_passphrase myrouter > wpa.conf
mypassphrase
You should end up with a file looking like this:

network={
    ssid="myrouter"
    #psk="mypassphrase"
    psk=8ada1f8dbea59704ac379538b4d9191f6a72390581b4cd7a72864cea685b1a7f
}
Getting connected

Now we will actually run wpa_supplicant to connect to the wireless network. First, if your router broadcasts its SSID (they all do by default), you probably want to make sure your wireless card can actually see it:

$ iwlist scan
You might have to run that as root to force a refresh.

Next, you will need to know three pieces of information:

Which wpa_supplicant wireless drivers to use for your card. Running wpa_supplicant --help lists the different drivers it has (under "drivers:"). As of 0.5.8, the useful choices are: wext, hostap, madwifi, atmel, ndiswrapper, and ipw (ipw is for old kernels only; >=2.6.13 should use wext). If you don't see a specific match for your card, try wext, as that's kind of the catch-all.
The network device of your card. This is usually eth1 or wlan0, but if you're unsure you can just run iwconfig. It will report "no wireless extensions" for non-wireless devices and will display some data for any wireless devices.
The path to the configuration file that you created in the previous step.
Now that you have this data, run (as root):

# wpa_supplicant -D[driver] -i[device] -c[/path/to/config]
There are no spaces between the options and parameters. Don't include the brackets as I just added those for clarity. For example, for my laptop it looks like this:

# wpa_supplicant -Dwext -ieth1 -c/root/wpa.conf
You can also run it in the background by using the -B option so that it doesn't take up your console.

Now you're associated with the network.

Getting online

To actually get online, you'll have to get an IP somehow. Most people will just want to get a dynamic IP from a DHCP server, probably the one built into the router. (I'm not going to cover setting a static IP and routing table because that's a beast in itself.)

To get a DHCP lease, first release whatever leases you're still holding onto (as root):

# dhclient -r
Then ask for a new lease (of course replacing eth1 with the name of your network device, the same one as you used in the previous section):

# dhclient eth1
You now have an IP, in theory at least. Happy surfing!
