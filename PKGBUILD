# $Id: PKGBUILD 78820 2012-10-25 06:47:28Z foutrelis $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>

pkgname=id3lib-rcc
pkgver=3.8.3
pkgrel=7
pkgdesc="id3lib with librcc patch"
arch=('i686' 'x86_64')
url="http://id3lib.sourceforge.net/"
license=('GPL')
depends=('libxml2' 'librcc' 'gcc-libs')
provides=('id3lib')
conflicts=('id3lib')
options=('!libtool')
source=(http://downloads.sourceforge.net/id3lib/id3lib-$pkgver.tar.gz
	http://downloads.sourceforge.net/rusxmms/id3lib-csa2.tar.bz2
	arch.patch
	id3lib-gcc4.patch)
md5sums=('19f27ddd2dda4b2d26a559a4f0f402a7'
         '608a475f119974c8f72406fd84e1030f'
         '8b503330d653578f75fc9f2bf3c3833d'
         '94191cf1fe6f5fd391d95a6de81a48b9')

build() {
  cd "${srcdir}"/id3lib-$pkgver

  patch -Np1 -i "${srcdir}"/id3lib/id3lib-ds-rcc.patch
  patch -Np1 -i "${srcdir}"/id3lib-gcc4.patch
  cd src
  patch -Np0 -i "${srcdir}"/arch.patch
  cd ..

  sed -i 's#iomanip.h##' configure
  sed -i 's|size_t size_t, size_t \*size_t|size_t s1, size_t *s2|' src/rccpatch.h

  ./configure --prefix=/usr
  make LDFLAGS=-lrcc
}

package() {
  cd "${srcdir}"/id3lib-$pkgver
  make DESTDIR="${pkgdir}" install
}
