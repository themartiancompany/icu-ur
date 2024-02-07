# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=74.1
pkgrel=1
pkgdesc="International Components for Unicode library"
arch=(
  x86_64
  arm
)
url="https://icu.unicode.org"
license=('custom:icu')
depends=('gcc-libs' 'glibc' 'sh')
makedepends=('python')
provides=(
  libicu
  libicu{data,i18n,io,test,tu,uc}.so
)
source=(https://github.com/unicode-org/icu/releases/download/release-${pkgver//./-}/icu4c-${pkgver//./_}-src.tgz{,.asc}
        ICU-22132.patch)
# https://github.com/unicode-org/icu/releases/download/release-74-1/SHASUM512.txt
sha512sums=('32c28270aa5d94c58d2b1ef46d4ab73149b5eaa2e0621d4a4c11597b71d146812f5e66db95f044e8aaa11b94e99edd4a48ab1aa8efbe3d72a73870cd56b564c2'
            'SKIP'
            '1178062ccfcf7ecc698c64132b3612e73f9c4b0bbfaa668ae2039f3eb4cb2722d0b08a9f45b057da10def7a308d5c8d14c0c644892e7f11092c9cc488c850ab7')
#validpgpkeys=('BA90283A60D67BA0DD910A893932080F4FB419E3') #  "Steven R. Loomis (filfla-signing) <srloomis@us.ibm.com>"
#validpgpkeys+=('9731166CD8E23A83BEE7C6D3ACA5DBE1FD8FABF1') #  "Steven R. Loomis (ICU Project) <srl@icu-project.org>"
#validpgpkeys+=('FFA9129A180D765B7A5BEA1C9B432B27D1BA20D7') # "Fredrik Roubert <fredrik@roubert.name>"
#validpgpkeys+=('E4098B78AFC94394F3F49AA903996C7C83F12F11') # "keybase.io/srl295 <srl295@keybase.io>"
#validpgpkeys+=('4569BBC09DA846FC91CBD21CE1BBA44593CF2AE0') # "Steven R. Loomis (codesign-qormi) <srloomis@us.ibm.com>"
#validpgpkeys=('0E51E7F06EF719FBD072782A5F56E5AFA63CCD33') #"Craig Cornelius (For use with ICU releases) <ccornelius@google.com>"
validpgpkeys=('3DA35301A7C330257B8755754058F67406EAA6AB') # Craig Cornelius <ccornelius@google.com>

prepare() {
  cd icu/source
  # Required fix for thunderbird 115 to show Calendar and sidebar properly
  # https://bugzilla.mozilla.org/show_bug.cgi?id=1843007
  # https://unicode-org.atlassian.net/browse/ICU-22132
  patch -Np1 < "../../ICU-22132.patch"
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
  install -Dm644 "${srcdir}"/icu/LICENSE "${pkgdir}"/usr/share/licenses/${pkgname}/LICENSE
}

# vim:set sw=2 sts=-1 et:
