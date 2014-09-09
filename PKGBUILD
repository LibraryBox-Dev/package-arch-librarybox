# Maintainer: Matthias Strubel <matthias.strubel@aod-rpg.de>
pkgname=librarybox-full
pkgver=2.1.0
pkgrel=3
#epoch=0
pkgdesc="Turns system into file distributing hotspot. Package used for creating the prepared images"
arch=('any')
url="http://librarybox.us"
license=('GPL')
groups=()
depends=(
 'python2' 
 'lighttpd'
 'bash'
 'start-stop-daemon'
 'iw'
 'hostapd'
 'dnsmasq'
 'bridge-utils'
 'radvd'
 'proftpd'
 'php'
 'php-cgi'
 'avahi'
 'php-sqlite'
 'lftp'
 'wget'
 'wireless_tools'
 'netctl'
 'perl'
 'iptables'
 'zip'
 'unzip'
 'cronie'
)

makedepends=()
checkdepends=()
provides=()
optdepends=( )
conflicts=()
replaces=()
backup=()
options=()
install=librarybox-full.install

#full url source=(ftp://ftp.gnu.org/gnu/$pkgname/$pkgname-$pkgver.tar.gz)
source=(librarybox-$pkgver.tar.gz
lan_dhcp
lan_piratebox_bridge
piratebox_bridge
librarybox.service
)

#####------- Build options
prepare(){
	cd $srcdir/librarybox/piratebox
	sed 's|DO_IFCONFIG="yes"|DO_IFCONFIG="no"|' -i conf/piratebox.conf
	sed 's|IPV6_ENABLE="no"|IPV6_ENABLE="yes"|' -i conf/ipv6.conf	
	sed 's|USE_APN="yes"|USE_APN="no"|'         -i conf/piratebox.conf
	sed 's|USE_DNSMASQ="no"|USE_DNSMASQ="yes"|' -i conf/piratebox.conf
#
	sed 's|DNSMASQ_INTERFACE="wlan0"|DNSMASQ_INTERFACE="br0"|' -i conf/piratebox.conf
	sed 's|BRIDGE="br-lan"|BRIDGE="br0"|' -i conf/piratebox.conf
	sed 's:NET=192.168.77:NET=192.168.1:'  -i conf/piratebox.conf
#
	sed 's:start-stop-daemon  \-S \-q \-x radvd:start-stop-daemon  \-S \-q \-x /usr/bin/radvd:' -i init.d/piratebox_alt
}

package(){
	mkdir -p $pkgdir/opt/
	cp -r    $srcdir/librarybox/piratebox $pkgdir/opt/

	mkdir -p $pkgdir/etc/systemd/system/
	cp     librarybox.service	$pkgdir/etc/systemd/system/
	
	

	# networking profiles
	mkdir -p $pkgdir/etc/netctl
	cp   lan_dhcp  $pkgdir/etc/netctl
	cp   lan_piratebox_bridge $pkgdir/etc/netctl
	cp   piratebox_bridge $pkgdir/etc/netctl
}

post_install(){
	groupadd nogroup
	usermod -a -G nogroup nobody
	
	netctl enable piratebox_bridge
	# TODO disable config, which is already active 
	netctl enable lan_piratebox_bridge

	#enable cron
	#enable avahi ?!

	ln -s /usr/bin/python2 /usr/bin/python
	
}
