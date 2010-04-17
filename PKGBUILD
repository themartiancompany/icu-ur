# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=4.4
pkgrel=2
pkgdesc="International Components for Unicode library"
arch=(i686 x86_64)
url="http://www.icu-project.org/"
license=('custom:"icu"')
depends=('gcc-libs' 'sh')
source=(#http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz)
	http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver/./_}-src.tgz
	icu.icu7567.libctest.patch)
md5sums=('36b77e68e73f0ee9f7bb862629e33342'
         'e3f89790605c739e693fc454c0332065')

build() {
  # fix missing libicutest.so.44, patch taken from Fedora
  cd ${srcdir}/icu
  patch -Np1 -i ${srcdir}/icu.icu7567.libctest.patch || return 1
  cd ${srcdir}/icu/source
  ./configure --prefix=/usr --sysconfdir=/etc --mandir=/usr/share/man
  make || return 1
  make -j1 DESTDIR=${pkgdir} install || return 1 

  # Install license
  install -Dm644 ${srcdir}/icu/license.html ${pkgdir}/usr/share/licenses/icu/license.html
}
