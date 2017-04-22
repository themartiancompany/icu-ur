# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

pkgname=icu
pkgver=58.2
pkgrel=2
pkgdesc="International Components for Unicode library"
arch=(i686 x86_64)
url="http://www.icu-project.org/"
license=('custom:icu')
depends=('gcc-libs>=4.7.1-5' 'sh')
#makedepends=('clang')
# no https available
source=(#http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver/./_}-src.tgz
	http://download.icu-project.org/files/${pkgname}4c/${pkgver}/${pkgname}4c-${pkgver//./_}-src.tgz
	icu-58.1-iterator-reset.patch
        changeset-39671-CVE-2017-7867+7868.patch)
# upstream offers md5sum checks, only asc file for md5sum check
md5sums=('fac212b32b7ec7ab007a12dff1f3aea1'
         '8c09ae284967def053e9579d64d0f83c'
         'cea722333992ad6ede88ebd0bd21cfcd')
sha256sums=('2b0a4410153a9b20de0e20c7d8b66049a72aef244b53683d0d7521371683da0c'
            '8034928bcff89eca84d8d0f22fa9b6bdba5e0608a984f64fe7afe41b91bbea97'
            'cf0c6f946d7336bd46857c52308fd67171918f24fcf19015b5a47a8d2fb8ca0c')

prepare() {
  cd icu/source
  # http://bugs.icu-project.org/trac/ticket/12827
  patch -Np4 -i "${srcdir}"/icu-58.1-iterator-reset.patch

  patch -Np4 -i "${srcdir}"/changeset-39671-CVE-2017-7867+7868.patch
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
  make -k check # passes all
}

package() {
  cd icu/source
  make -j1 DESTDIR=${pkgdir} install

  # Install license
  install -Dm644 ${srcdir}/icu/license.html ${pkgdir}/usr/share/licenses/icu/license.html
}
