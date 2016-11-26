# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=58.1
pkgrel=1
pkgdesc="International Components for Unicode library"
arch=(i686 x86_64)
url="http://www.icu-project.org/"
license=('custom:icu')
depends=('gcc-libs>=4.7.1-5' 'sh')
#makedepends=('clang')
# no https available
source=(#http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver/./_}-src.tgz
	http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz)
#	icu.8198.revert.icu5431.patch)
# upstream offers md5sum checks, only asc file for md5sum check
md5sums=('1901302aaff1c1633ef81862663d2917')
#         'ebd5470fc969c75e52baf4af94a9ee82')

# that file is no more present in current release, asume the bug to be fixed.
#prepare() {
#  cd icu/source
#  # fix Malayalam encoding https://bugzilla.redhat.com/show_bug.cgi?id=654200
#  patch -Rp3 -i ${srcdir}/icu.8198.revert.icu5431.patch
#}

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
  make -k check # passes all
}

package() {
  cd icu/source
  make -j1 DESTDIR=${pkgdir} install

  # Install license
  install -Dm644 ${srcdir}/icu/license.html ${pkgdir}/usr/share/licenses/icu/license.html
}
