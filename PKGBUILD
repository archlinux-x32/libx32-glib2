# $Id: PKGBUILD 109538 2014-04-15 14:55:48Z bluewind $
# Maintainer:  Ionut Biru <ibiru@archlinux.org>
# Contributor: Pierre Schmitz <pierre@archlinux.de>
# Contributor: Mikko Seppälä <t-r-a-y@mbnet.fi>

_pkgbasename=glib2
pkgname=lib32-$_pkgbasename
pkgver=2.40.0
pkgrel=1
pkgdesc="Common C routines used by GTK+ 2.4 and other libs (32-bit)"
url="http://www.gtk.org/"
arch=('x86_64')
license=('LGPL')
depends=('lib32-pcre' 'lib32-zlib' 'lib32-libdbus' lib32-libffi $_pkgbasename)
makedepends=('gcc-multilib' python2)
options=('!libtool' '!docs')
source=(http://ftp.gnome.org/pub/GNOME/sources/glib/${pkgver%.*}/glib-${pkgver}.tar.xz)
sha256sums=('0d27f195966ecb1995dcce0754129fd66ebe820c7cd29200d264b02af1aa28b5')

build() {
  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  cd "${srcdir}/glib-${pkgver}"
  PYTHON=/usr/bin/python2 ./configure --prefix=/usr --sysconfdir=/etc --libdir=/usr/lib32 \
      --enable-static --enable-shared --with-pcre=system --disable-fam
  make
}

package() {
  cd "${srcdir}/glib-${pkgver}"
  make DESTDIR="${pkgdir}" install
  rm -rf "${pkgdir}"/{etc,usr/{share,include}}

  cd "${pkgdir}"/usr/bin
  mv gio-querymodules gio-querymodules-32
  rm -f gdbus glib* gobject-query gsettings gtester*
  rm -rf "$pkgdir"/usr/lib32/gdbus-2.0
  find "$pkgdir/usr/bin" -type f -not -name gio-querymodules-32 -delete
}
