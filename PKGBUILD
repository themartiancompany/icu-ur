# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=64.1
pkgrel=1
pkgdesc="International Components for Unicode library"
arch=(x86_64)
url="http://www.icu-project.org/"
license=('custom:icu')
depends=('gcc-libs' 'sh')
makedepends=('python')
#makedepends=('clang')
# no https available
source=(#http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver/./_}-src.tgz
        https://ssl.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz{,.asc})
# https://ssl.icu-project.org/files/icu4c/62.1/SHASUM512.txt
sha512sums=('5eca8342d8bdf902689243506643e04512744b33962687e118f6810af6f7fd073678f67b991d2ae9139d257713b63abb4222b96687234df01ad5ff62df16ede0'
            'SKIP')
validpgpkeys=('BA90283A60D67BA0DD910A893932080F4FB419E3') #  "Steven R. Loomis (filfla-signing) <srloomis@us.ibm.com>" 
validpgpkeys+=('9731166CD8E23A83BEE7C6D3ACA5DBE1FD8FABF1') #  "Steven R. Loomis (ICU Project) <srl@icu-project.org>" 
validpgpkeys+=('FFA9129A180D765B7A5BEA1C9B432B27D1BA20D7') # "Fredrik Roubert <fredrik@roubert.name>"
validpgpkeys+=('E4098B78AFC94394F3F49AA903996C7C83F12F11') # "keybase.io/srl295 <srl295@keybase.io>"

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
