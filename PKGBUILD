# Contributor: Tobias Powalowski  <tpowa@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>
# Contributor: Alexander Baldeck <alexander@archlinux.org>
# Contributor: Kaspar Bumke <kaspar.bumke@gmail.com>
# Contributor: Matthew Phipps <mphipps1@umd.edu>

pkgname=synaptics-xrandr
_pkgname=xf86-input-synaptics
pkgver=1.5.99
pkgrel=0.2
pkgdesc="Synaptics driver for notebook touchpads with patch to enable axis rotation."
arch=('i686' 'x86_64')
license=('custom')
url="http://xorg.freedesktop.org/"
depends=('libxtst')
makedepends=('xorg-server-devel>=1.11.99.902' 'libxi' 'libx11')
conflicts=('xorg-server<1.11.99.902')
replaces=('synaptics')
provides=('synaptics')
conflicts=('synaptics')
groups=('xorg-drivers' 'xorg')
options=(!libtool)
backup=('etc/X11/xorg.conf.d/10-synaptics.conf')
source=(#http://xorg.freedesktop.org/releases/individual/driver/${pkgname}-${pkgver}.tar.bz2
		http://cgit.freedesktop.org/xorg/driver/xf86-input-synaptics/snapshot/xf86-input-synaptics-${_gitver}.tar.gz
        10-synaptics.conf)
md5sums=('9676852145949e9d9afbd548057f37ab'
         '3b81a81b958dfe3cac3cdef7ee85f1ce')

build() {
#  cd "${srcdir}/${pkgname}-${pkgver}"
  cd ${srcdir}/${_pkgname}*
  autoreconf -fi
  ./configure --prefix=/usr
  make
}

package() {
  #cd "${srcdir}/${pkgname}-${pkgver}"
  cd ${srcdir}/${_pkgname}*
  make DESTDIR="${pkgdir}" install
  install -m755 -d "${pkgdir}/etc/X11/xorg.conf.d"
  install -m644 "${srcdir}/10-synaptics.conf" "${pkgdir}/etc/X11/xorg.conf.d/"
  install -m755 -d "${pkgdir}/usr/share/licenses/${_pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${_pkgname}/"

  rm -rf "${pkgdir}/usr/share/X11"
}
