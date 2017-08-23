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
        https://ssl.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz{,.asc})
# upstream offers md5sum checks, only asc file for md5sum check
md5sums=('54923fa9fab5b2b83f235fb72523de37'
         'SKIP')
sha256sums=('7132fdaf9379429d004005217f10e00b7d2319d0fea22bdfddef8991c45b75fe'
            'SKIP')
validpgpkeys=('BA90283A60D67BA0DD910A893932080F4FB419E3') #  "Steven R. Loomis (filfla-signing) <srloomis@us.ibm.com>" 

prepare() {
  cd icu/source
  # https://ssl.icu-project.org/trac/ticket/13329
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
  install -Dm644 ${srcdir}/icu/LICENSE ${pkgdir}/usr/share/licenses/icu/LICENSE
}
