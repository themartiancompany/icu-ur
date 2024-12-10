## SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Art Gramlich <art@gramlich-net.com>

_os="$( \
  uname \
    -o)"
_py="python"
_pkg=icu
pkgname="${_pkg}"
pkgver=76.1
_pkgver="${pkgver//./-}"
pkgrel=1
pkgdesc="International Components for Unicode library"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'armv7l'
  'armv6l'
  'mips'
  'powerpc'
  'pentium4'
  'i686'
)
url="https://${_pkg}.unicode.org"
license=(
  "custom:${_pkg}"
)
depends=()
if [[ "${_os}" == "GNU/Linux" ]]; then
  depends+=(
    'gcc-libs'
    'glibc'
    'sh'
  )
if [[ "${_os}" == "Android" ]]; then
  depends+=(
    'ndk-sysroot'
    'bash'
  )
fi
makedepends=(
  "${_py}"
)
provides=(
  "lib${_pkg}=${pkgver}"
  "lib${_pkg}"{"data","i18n","io","test","tu","uc"}".so"
)
conflicts=(
  "lib${_pkg}"
)
_http="https://github.com"
_ns="unicode-org"
_url="${_http}/${_ns}/${_pkg}"
_dl="${_url}/releases/download"
source=(
  "${_dl}/release-${_pkgver}/${_pkg}4c-${pkgver//./_}-src.tgz"{,.asc}
  "ICU-22132.patch"
)
# ${_dl}/release-76-1/SHASUM512.txt
sha512sums=(
  'b702ab62fb37a1574d5f4a768326d0f8fa30d9db5b015605b5f8215b5d8547f83d84880c586d3dcc7b6c76f8d47ef34e04b0f51baa55908f737024dd79a42a6c'
  'SKIP'
  '1178062ccfcf7ecc698c64132b3612e73f9c4b0bbfaa668ae2039f3eb4cb2722d0b08a9f45b057da10def7a308d5c8d14c0c644892e7f11092c9cc488c850ab7'
)
validpgpkeys=(
  # Steven R. Loomis (filfla-signing) <srloomis@us.ibm.com>
  # 'BA90283A60D67BA0DD910A893932080F4FB419E3'
  # Steven R. Loomis (ICU Project) <srl@icu-project.org>
  # '9731166CD8E23A83BEE7C6D3ACA5DBE1FD8FABF1'
  # Fredrik Roubert <fredrik@roubert.name>
  # 'FFA9129A180D765B7A5BEA1C9B432B27D1BA20D7'
  # keybase.io/srl295 <srl295@keybase.io>
  # 'E4098B78AFC94394F3F49AA903996C7C83F12F11'
  # Steven R. Loomis (codesign-qormi) <srloomis@us.ibm.com>
  # '4569BBC09DA846FC91CBD21CE1BBA44593CF2AE0'
  # Craig Cornelius (For use with ICU releases) <ccornelius@google.com>
  # '0E51E7F06EF719FBD072782A5F56E5AFA63CCD33'
  # Craig Cornelius <ccornelius@google.com>
  '3DA35301A7C330257B8755754058F67406EAA6AB'
) 
prepare() {
  cd \
    "${_pkg}/source"
  # Required fix for thunderbird 115 to show Calendar and sidebar properly
  # https://bugzilla.mozilla.org/show_bug.cgi?id=1843007
  # https://unicode-org.atlassian.net/browse/ICU-22132
  patch \
    -Np1 < \
    "../../ICU-22132.patch"
}

build() {
  local \
    _configure_opts=()
  cd \
    "${_pkg}/source"
  _configure_opts=(
    --prefix=/usr
    --sysconfdir=/etc
    --mandir=/usr/share/man
    --sbindir=/usr/bin
  )
  ./configure \
    "${_configure_opts[@]}"
  make
}

check() {
  cd \
    "${_pkg}/source"
  make \
    -k \
    check
}

package() {
  cd \
    "${_pkg}/source"
  make \
    -j1 \
    DESTDIR="${pkgdir}" \
    install
  # Install license
  install \
    -Dm644 \
    "${srcdir}/${_pkg}/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set sw=2 sts=-1 et:
