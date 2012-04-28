# Maintainer: Matt Phipps <mphipps1@umd.edu>
# Contributor: Matthew Monaco <net 0x01b dgbaley27>
# Contributor: Tobias Powalowski  <tpowa@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>
# Contributor: Alexander Baldeck <alexander@archlinux.org>
# Contributor: Kaspar Bumke <kaspar.bumke@gmail.com>

_pkgname=xf86-input-synaptics
pkgname=$_pkgname-xrandr
pkgver=1.5.99.904
pkgrel=1
pkgdesc="Synaptics driver for notebook touchpads (with Rotation support)."
arch=('i686' 'x86_64')
license=('custom')
url="https://github.com/garaden/synaptics-xrandr/"
depends=('libxtst' 'mtdev')
makedepends=('xorg-server-devel>=1.11.99.902' 'libxi' 'libx11')
conflicts=('xorg-server<1.11.99.902')
replaces=('synaptics')
provides=('synaptics' "${_pkgname}")
conflicts=('synaptics' "${_pkgname}")
groups=('xorg-drivers' 'xorg')
options=(!libtool)
backup=('etc/X11/xorg.conf.d/50-synaptics.conf')
source=(http://xorg.freedesktop.org/releases/individual/driver/${_pkgname}-${pkgver}.tar.bz2
        0001-Add-rotation-property-param-and-docs.patch
        0002-Enable-rotation-on-each-backend.patch)
md5sums=('8c07650a79b160c8f04470219bf1bd84'
         'a79e16dfc57f1605375f219542b4c481'
         '717e00920693105e5a7497ac4f00caa6')

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  for p in ../*.patch; do
    msg2 "Applying patch: $p"
    patch -p1 -i "$p"
  done
  ./configure --prefix=/usr
  make
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -m755 -d "${pkgdir}/etc/X11/xorg.conf.d"
  install -m644 "conf/50-synaptics.conf" "${pkgdir}/etc/X11/xorg.conf.d/"
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/"

  rm -rf "${pkgdir}/usr/share/X11"
}
