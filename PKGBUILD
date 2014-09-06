# Maintainer: Matthias Strubel <matthias.strubel@aod-rpg.de>
pkgname=librarybox
pkgver=2.1.0
pkgrel=1
#epoch=0
pkgdesc="Turns system into file distributing hotspot. Initial Package with minimum configuration"
arch=('any')
url="http://librarybox.us"
license=('GPL')
groups=()
depends=(
 'python2' 
 'lighttpd'
 'bash'
)
#depends not in my repository:
#start-stop-daemon

makedepends=()
checkdepends=()
provides=()
optdepends=(
'iw: needed for some rare cards for early initialization' 
'hostapd: needed to run a wifi-hotspot'
'dnsmasq: needed to server IPs and DNS-based redirection'
'bridge-utils: enabled possibility to add AP-wifi during start to existing bridge'
'radvd: possibility to distribute IPv6 addresses'
)
#proftpd

conflicts=()
replaces=()
backup=()
options=()

#full url source=(ftp://ftp.gnu.org/gnu/$pkgname/$pkgname-$pkgver.tar.gz)
source=($pkgname-$pkgver.tar.gz)


#optional
#'core/iw'
#'community/hostapd'
#'community/minidlna'
#'extra/dnsmasq'
#'core/bridge-utils'
# radvd
## not 100% needed 'core/netctl'


#####------- Build options
prepare(){
	cd $srcdir/librarybox/piratebox
	sed 's:DO_IFCONFIG="yes":DO_IFCONFIG="no":' -i conf/piratebox.conf
	sed 's|IPV6_ENABLE="yes"|IPV6_ENABLE="no"|' -i conf/ipv6.conf	
	sed 's|DO_IFCONFIG="yes"|DO_IFCONFIG="no"|' -i conf/piratebox.conf
	sed 's|USE_APN="yes"|USE_APN="no"|'         -i conf/piratebox.conf
	sed 's|USE_DNSMASQ="yes"|USE_DNSMASQ="no"|' -i conf/piratebox.conf
}

package(){
	mkdir -p $pkgdir/opt/
	cp -r    $srcdir/librarybox/piratebox $pkgdir/opt/
}
