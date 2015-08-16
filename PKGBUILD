# $Id: PKGBUILD 63997 2012-02-08 18:53:23Z pschmitz $
# Maintainer: Jan "heftig" Steffens <jan.steffens@gmail.com>

_pkgbasename=libsndfile
pkgname=libx32-$_pkgbasename
pkgver=1.0.25
pkgrel=2.1
pkgdesc="A C library for reading and writing files containing sampled sound (x32 ABI)"
arch=('x86_64')
url="http://www.mega-nerd.com/libsndfile"
license=('LGPL')
depends=('libx32-flac' 'libx32-libvorbis' $_pkgbasename)
makedepends=('libx32-alsa-lib' 'gcc-multilib-x32')
options=('!libtool')
source=(http://www.mega-nerd.com/libsndfile/files/${_pkgbasename}-${pkgver}.tar.gz)
md5sums=('e2b7bb637e01022c7d20f95f9c3990a2')
sha1sums=('e95d9fca57f7ddace9f197071cbcfb92fa16748e')

build() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"

  export CC="gcc -mx32"
  export CXX="g++ -mx32"
  export PKG_CONFIG_PATH="/usr/libx32/pkgconfig"

  export GETCONF="getconf -v POSIX_V7_ILP32_OFFBIG"
  export GETCONF_DIR="/usr/libx32/getconf"

  ./configure --prefix=/usr --disable-sqlite --libdir=/usr/libx32
  make -C src
}

package() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  make -C src DESTDIR="${pkgdir}" install
  make DESTDIR="$pkgdir" install-pkgconfigDATA

  rm -rf "$pkgdir/usr/include"
}
