# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=hatch-vcs
_Pkg=sphinx-doc-devhelp
pkgname="${_py}-${_pkg}"
pkgver=0.4.0
_commit=e186a8b5d97dd9c9f93ae6015139b55411d9011b
pkgrel=1
pkgdesc="Hatch plugin for versioning with your preferred VCS"
_http="https://github.com"
_ns="ofek"
url="${_http}/${_ns}/${_pkg}"
license=('MIT')
arch=(
  'any'
)
depends=(
  'python-hatchling'
  'python-setuptools-scm'
)
makedepends=(
  'git'
  'python-build'
  'python-installer'
)
checkdepends=(
  'python-pytest'
)
source=(
  "git+${url}.git#commit=${_commit}"
)
sha512sums=(
  'SKIP'
)

build() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      build \
    -nw
}

check() {
  local \
    site_packages
  site_packages=$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      installer \
    --destdir=tmp_install \
    dist/*.whl
  PYTHONPATH="${PWD}/tmp_install${site_packages}" \
  pytest
}

package() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    LICENSE.txt \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}
