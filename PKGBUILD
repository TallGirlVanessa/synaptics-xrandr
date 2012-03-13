# Contributor: Tobias Powalowski  <tpowa@archlinux.org>
# Contributor: Thomas Bächler <thomas@archlinux.org>
# Contributor: Alexander Baldeck <alexander@archlinux.org>
# Contributor: Kaspar Bumke <kaspar.bumke@gmail.com>

pkgname=synaptics-xrandr
_pkgname=xf86-input-synaptics
pkgver=1.4.1
pkgrel=1
pkgdesc="Synaptics driver for notebook touchpads with patch to enable axis rotation."
arch=(i686 x86_64)
license=('custom')
url="http://xorg.freedesktop.org/"
depends=('libxtst')
makedepends=('xorg-server-devel' 'libxi' 'libx11')
conflicts=('xorg-server<1.10.0')
replaces=('synaptics')
provides=('synaptics')
conflicts=('synaptics')
groups=('xorg-drivers' 'xorg')
options=(!libtool)
backup=('etc/X11/xorg.conf.d/10-synaptics.conf')
source=(http://xorg.freedesktop.org/releases/individual/driver/${_pkgname}-${pkgver}.tar.bz2 10-synaptics.conf synaptics-xrandr.patch)

sha1sums=('e41201476f4bc8658291808d2d6ef2e0535179ae'
          '68e1f4ef5e1038231d210eb422fa4d18c5922f0f'
          '38fa5f885386206eb3c0fed64035d15209dffd1c')

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  patch -p1 < ../synaptics-xrandr.patch || return 1
  ./configure --prefix=/usr
  make
}
package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -m755 -d "${pkgdir}/etc/X11/xorg.conf.d"
  install -m644 "${srcdir}/10-synaptics.conf" "${pkgdir}/etc/X11/xorg.conf.d/"
  install -m755 -d "${pkgdir}/usr/share/licenses/${_pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${_pkgname}/"

  rm -rf "${pkgdir}/usr/share/X11"
}
