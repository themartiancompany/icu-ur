# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=65.1
pkgrel=2
pkgdesc="International Components for Unicode library"
arch=(x86_64)
url="http://site.icu-project.org/home"
license=('custom:icu')
depends=('gcc-libs' 'sh')
makedepends=('python')
#makedepends=('clang')
# no https available
source=(https://github.com/unicode-org/icu/releases/download/release-${pkgver//./-}/${pkgname}4c-${pkgver//./_}-src.tgz{,.asc}
        icu-65.1-initialized-buffer-uloc_getKeywordValue.patch::https://github.com/unicode-org/icu/commit/fab4c3c719.patch)
# https://github.com/unicode-org/icu/releases/download/release-65-1/SHASUM512.txt
sha512sums=('8f1ef33e1f4abc9a8ee870331c59f01b473d6da1251a19ce403f822f3e3871096f0791855d39c8f20c612fc49cda2c62c06864aa32ddab2dbd186d2b21ce9139'
            'SKIP'
            '8898fe0fa9805304cd2fc02c00ab1131861836f4d11887f82450c2378666cb03bce0c5038d3f0bdcdd1c1cdee2a00a61ef85602ed0e0c74ad2e58578b1940123')
validpgpkeys=('BA90283A60D67BA0DD910A893932080F4FB419E3') #  "Steven R. Loomis (filfla-signing) <srloomis@us.ibm.com>" 
validpgpkeys+=('9731166CD8E23A83BEE7C6D3ACA5DBE1FD8FABF1') #  "Steven R. Loomis (ICU Project) <srl@icu-project.org>" 
validpgpkeys+=('FFA9129A180D765B7A5BEA1C9B432B27D1BA20D7') # "Fredrik Roubert <fredrik@roubert.name>"
validpgpkeys+=('E4098B78AFC94394F3F49AA903996C7C83F12F11') # "keybase.io/srl295 <srl295@keybase.io>"

prepare() {
  cd icu
  # https://unicode-org.atlassian.net/browse/ICU-20884
  patch -Np2 -i ../icu-65.1-initialized-buffer-uloc_getKeywordValue.patch
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
  make -j1 DESTDIR="${pkgdir}" install

  # Install license
  install -Dm644 "${srcdir}"/icu/LICENSE "${pkgdir}"/usr/share/licenses/icu/LICENSE
}
