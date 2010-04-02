# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=4.4
pkgrel=1
pkgdesc="International Components for Unicode library"
arch=(i686 x86_64)
url="http://www.icu-project.org/"
license=('custom:"icu"')
depends=('gcc-libs' 'sh')
source=(#http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz)
	http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver/./_}-src.tgz)
md5sums=('36b77e68e73f0ee9f7bb862629e33342')

build() {
  cd ${srcdir}/icu/source
  ./configure --prefix=/usr --sysconfdir=/etc --mandir=/usr/share/man
  make || return 1
  make -j1 DESTDIR=${pkgdir} install || return 1 

  # Install license
  install -Dm644 ${srcdir}/icu/license.html ${pkgdir}/usr/share/licenses/icu/license.html
}
