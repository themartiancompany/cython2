# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Danilo J. S. Bellini <danilo dot bellini at gmail dot com>
# Contributor: Antonio Rojas <arojas@archlinux.org>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Igor Scabini <furester @ gmail.com>

_py="python2"
_pkg="cython"
pkgname="${_pkg}2"
pkgver=0.29.37
pkgrel=1
pkgdesc='C-Extensions for Python 2'
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'armv7l'
  'armv6l'
  'mips'
  'powerpc'
  'i686'
)
url="https://${_pkg}.org"
_http="https://github.com"
_ns="${_pkg}"
_url="${_http}/${_ns}/${_pkg}"
license=(
  'APACHE'
)
makedepends=(
  "${_py}-setuptools"
)
depends=(
  "${_py}"
)
source=(
  "${pkgname}-${pkgver}.tar.gz::${_url}/archive/refs/tags/${pkgver}.tar.gz"
)
sha256sums=(
  '824eb14045d85c5af677536134199dd6709db8fb0835452fd2d54bc3c8df8887'
)

prepare() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  # Update shebangs in scripts to call "python2" instead of "python"
  find \
    -name \
      "*.py*" \
    -exec \
      sed \
        -i \
	  '1s/python\s*$/python2/' \
	'{}' \;
}

build() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  "${_py}" \
    setup.py \
      build
}

package() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  "${_py}" \
    setup.py \
      install \
        --root="${pkgdir}" \
	--optimize=1 \
	--skip-build
  find \
    "${pkgdir}/usr/bin" \
    -type \
      "f" \
    -not \
      -name \
        '*2' \
    -exec \
      mv \
        '{}'{,2} \;
  install \
    -Dm644 \
    "LICENSE.txt" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.txt"
}
