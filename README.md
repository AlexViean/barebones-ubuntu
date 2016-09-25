<h1>Install barebones Ubuntu on Asus K501UB</h1>
<h2>Pre-installation</h2>
<ol>
<li>Download Lubuntu Alternate Installer ISO file</li>
<p>http://cdimages.ubuntu.com/lubuntu/releases/xenial/release/</p>
</ol>
<h3>Install Unity</h3>
<p>sudo apt-get install ubuntu-desktop --no-install-recommends</p>
<h3>Post Installation</h3>
<p>sudo apt-get install menu hud indicator-session unity-lens-applications unity-lens-files xserver-xorg-video-all policykit-desktop-privileges</p>

# Fix airplane mode
<p>sudo echo "blacklist asus_nb_wmi" >> /etc/modprobe.d/blacklist.conf</p>

# Install nVIDIA driver
<p>sudo add-apt-repository ppa:graphics-drivers/ppa</p>
<p>sudo apt-get update</p>
<p>sudo apt-get install nvidia-prime nvidia-367 bumblebee</p>
