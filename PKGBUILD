# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

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
_pkg=sphinxcontrib-serializinghtml
_Pkg=sphinx-doc-serializinghtml
pkgname="${_py}-${_pkg}"
pkgver=2.0.0
pkgrel=1
pkgdesc='Sphinx extension which outputs "serialized" HTML files (json and pickle)'
arch=(
  any
)
_http="https://github.com"
_ns="sphinx-doc"
url="${_http}/${_ns}/${_pkg}"
license=(
  BSD-2-Clause
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  git
  "${_py}-build"
  "${_py}-flit-core"
  "${_py}-installer"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-sphinx"
)
source=(
  "${_pkg}-${pkgver}::git+${url}.git#tag=$pkgver"
)
b2sums=(
  'da9c959497948b308869321ad8e3ff6baae93948f61180c1b5090b8c453cba12d18147b495653f981fd33a1805829427ae44b135f2bde417e4545ff2c0d77d4b'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  PYTHONPATH="sphinxcontrib/devhelp:${PYTHONPATH}" \
  pytest
}

package() {
  local \
    _site_packages
  _site_packages=$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  # Symlink license file
  install \
    -dm755 \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${_site_packages}/${_Pkg}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
