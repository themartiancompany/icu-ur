# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=63.1
pkgrel=2
pkgdesc="International Components for Unicode library"
arch=(x86_64)
url="http://www.icu-project.org/"
license=('custom:icu')
depends=('gcc-libs' 'sh')
#makedepends=('clang')
# no https available
source=(#http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver/./_}-src.tgz
        https://ssl.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz{,.asc}
        icu-63.1-checkImpl.patch::https://github.com/unicode-org/icu/commit/9ec2c332c1.patch)
# https://ssl.icu-project.org/files/icu4c/62.1/SHASUM512.txt
sha512sums=('9ab407ed840a00cdda7470dcc4c40299a125ad246ae4d019c4b1ede54781157fd63af015a8228cd95dbc47e4d15a0932b2c657489046a19788e5e8266eac079c'
            'SKIP'
            'ce1ec3c14f80658dad6127a037dfc0b21b4bff578240e7c8d8ca8c86cd8a5fe06b527e6a61db0aa303b708f1224f1401a59ad2b175c9640c375d37f138b4c523')
validpgpkeys=('BA90283A60D67BA0DD910A893932080F4FB419E3') #  "Steven R. Loomis (filfla-signing) <srloomis@us.ibm.com>" 
validpgpkeys+=('9731166CD8E23A83BEE7C6D3ACA5DBE1FD8FABF1') #  "Steven R. Loomis (ICU Project) <srl@icu-project.org>" 
validpgpkeys+=('FFA9129A180D765B7A5BEA1C9B432B27D1BA20D7') # "Fredrik Roubert <fredrik@roubert.name>"
validpgpkeys+=('E4098B78AFC94394F3F49AA903996C7C83F12F11') # "keybase.io/srl295 <srl295@keybase.io>"

prepare() {
  cd icu/source
  # https://unicode-org.atlassian.net/browse/ICU-20208
  patch -Np3 -i ${srcdir}/icu-63.1-checkImpl.patch
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
  make -k check
}

package() {
  cd icu/source
  make -j1 DESTDIR=${pkgdir} install

  # Install license
  install -Dm644 ${srcdir}/icu/LICENSE ${pkgdir}/usr/share/licenses/icu/LICENSE
}
