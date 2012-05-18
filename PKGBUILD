# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=49.1.1
pkgrel=2
pkgdesc="International Components for Unicode library"
arch=(i686 x86_64)
url="http://www.icu-project.org/"
license=('custom:"icu"')
depends=('gcc-libs' 'sh')
source=(#http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver/./_}-src.tgz
	    http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz
	    icu.8198.revert.icu5431.patch
	    fix_broken_regex.diff)
md5sums=('7c53f83e0327343f4060c0eb83842daf'
         'ebd5470fc969c75e52baf4af94a9ee82'
         '5bbcd600fdf9b35cbd89a06cab522f3f')

build() {
  cd ${srcdir}/icu/source
  # fix Malayalam encoding https://bugzilla.redhat.com/show_bug.cgi?id=654200
  patch -Rp3 -i ${srcdir}/icu.8198.revert.icu5431.patch
  # patch broken regex  - https://bugs.archlinux.org/task/29700 / http://bugs.icu-project.org/trac/ticket/9276
  patch -Np0 -i ${srcdir}/fix_broken_regex.diff
  ./configure --prefix=/usr \
	--sysconfdir=/etc \
	--mandir=/usr/share/man
  make
}

package() {
  cd ${srcdir}/icu/source
  make -j1 DESTDIR=${pkgdir} install

  # Install license
  install -Dm644 ${srcdir}/icu/license.html ${pkgdir}/usr/share/licenses/icu/license.html
}
