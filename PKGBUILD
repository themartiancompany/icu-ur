# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=61.1
pkgrel=1
pkgdesc="International Components for Unicode library"
arch=(x86_64)
url="http://www.icu-project.org/"
license=('custom:icu')
depends=('gcc-libs' 'sh')
#makedepends=('clang')
# no https available
source=(#http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver/./_}-src.tgz
        https://ssl.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz{,.asc})
# upstream offers md5sum checks, only asc file for md5sum check
md5sums=('68fe38999fef94d622bd6843d43c0615'
         'SKIP')
validpgpkeys=('BA90283A60D67BA0DD910A893932080F4FB419E3') #  "Steven R. Loomis (filfla-signing) <srloomis@us.ibm.com>" 
validpgpkeys+=('9731166CD8E23A83BEE7C6D3ACA5DBE1FD8FABF1') #  "Steven R. Loomis (ICU Project) <srl@icu-project.org>" 
validpgpkeys+=('FFA9129A180D765B7A5BEA1C9B432B27D1BA20D7') # "Fredrik Roubert <fredrik@roubert.name>"

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
  make -k check
}

package() {
  cd icu/source
  make -j1 DESTDIR=${pkgdir} install

  # Install license
  install -Dm644 ${srcdir}/icu/LICENSE ${pkgdir}/usr/share/licenses/icu/LICENSE
}
