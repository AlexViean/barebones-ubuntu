<h1>Install barebones Ubuntu on Asus K501UB</h1>
<h2>Pre-installation</h2>
<ol>
<li>Download Lubuntu Alternate Installer ISO file</li>
<p>http://cdimages.ubuntu.com/lubuntu/releases/xenial/release/</p>
</ol>
<h2>To install command-line Ubuntu</h2>
<p>Too easy</p>
<ul><h3><li>Install Unity</li></h3>
<p>sudo apt-get install ubuntu-desktop --no-install-recommends</p>
<p>sudo apt-get install menu hud indicator-session unity-lens-applications unity-lens-files policykit-desktop-privileges</p>
<p># Install this for Virtual Machine only: xserver-xorg-video-all</p>
<h3><li>Install MATE Core</li></h3>
<p>sudo apt-get install mate-core lightdm</p></ul>
<h2>Post Installation</h2>
<ul>
<h3><li>To fix airplane mode</li></h3>
<p>sudo echo "blacklist asus_nb_wmi" >> /etc/modprobe.d/blacklist.conf</p>

<h3><li>To install nVIDIA driver</li></h3>
<p>sudo add-apt-repository ppa:graphics-drivers/ppa</p>
<p>sudo apt-get update</p>
<p>sudo apt-get install nvidia-prime nvidia-367 bumblebee</p>

<h3><li>To hide fsck message</li></h3>
<p>Add loglevel=3 to /etc/default/grub</p>
<h3><li>Install using Synaptic</li></h3>
<p>software-properties</p></ul>
