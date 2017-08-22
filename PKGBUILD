# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=59.1
pkgrel=2
pkgdesc="International Components for Unicode library"
arch=(i686 x86_64)
url="http://www.icu-project.org/"
license=('custom:icu')
depends=('gcc-libs' 'sh')
#makedepends=('clang')
# no https available
source=(#http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver/./_}-src.tgz
	http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz)
# upstream offers md5sum checks, only asc file for md5sum check
md5sums=('54923fa9fab5b2b83f235fb72523de37')
sha256sums=('7132fdaf9379429d004005217f10e00b7d2319d0fea22bdfddef8991c45b75fe')

prepare() {
  cd icu/source
  sed -i 's/xlocale/locale/' i18n/digitlst.cpp
}

build() {
  cd icu/source
  ./configure --prefix=/usr \
	--sysconfdir=/etc \
	--mandir=/usr/share/man \
	--sbindir=/usr/bin
  make
}

check() {
  cd icu/source
  # some tests are broken when crossbuilding i686
  if [ "$CARCH" = "x86_64" ]; then
    make -k check
	else
    make -k check || /bin/true
  fi
}

package() {
  cd icu/source
  make -j1 DESTDIR=${pkgdir} install

  # Install license
  install -Dm644 ${srcdir}/icu/license.html ${pkgdir}/usr/share/licenses/icu/license.html
}
