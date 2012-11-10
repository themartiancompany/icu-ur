# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=50.1
pkgrel=2
pkgdesc="International Components for Unicode library"
arch=(i686 x86_64)
url="http://www.icu-project.org/"
license=('custom:"icu"')
depends=('gcc-libs>=4.7.1-5' 'sh')
source=(#http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver/./_}-src.tgz
	    http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz
	    icu.8198.revert.icu5431.patch changeset_32780.diff)
md5sums=('cf7bf9e56aa6c2057a8b6f464046483e'
         'ebd5470fc969c75e52baf4af94a9ee82'
         '58f4b655e40dddc8e316600019b491b2')

build() {
  cd ${srcdir}/icu/source

  # fix Malayalam encoding https://bugzilla.redhat.com/show_bug.cgi?id=654200
  patch -Rp3 -i ${srcdir}/icu.8198.revert.icu5431.patch

  # fix building clients without c++11 http://bugs.icu-project.org/trac/changeset/32780
  patch -Np4 -i ${srcdir}/changeset_32780.diff

  ./configure --prefix=/usr \
	--sysconfdir=/etc \
	--mandir=/usr/share/man
  make
}

check() {
  cd "$srcdir/icu/source"
  make -k check # passes all
}

package() {
  cd ${srcdir}/icu/source
  make -j1 DESTDIR=${pkgdir} install

  # Install license
  install -Dm644 ${srcdir}/icu/license.html ${pkgdir}/usr/share/licenses/icu/license.html
}
