# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

_name=sphinxcontrib_serializinghtml
pkgname=python-sphinxcontrib-serializinghtml
pkgver=1.1.7
pkgrel=1
pkgdesc='Sphinx extension which outputs "serialized" HTML files (json and pickle)'
arch=('any')
url=https://github.com/sphinx-doc/sphinxcontrib-serializinghtml
license=('BSD')
makedepends=('python-build' 'python-flit-core' 'python-installer')
checkdepends=('python-pytest' 'python-sphinx')
source=("https://files.pythonhosted.org/packages/source/${_name::1}/$_name/$_name-$pkgver.tar.gz")
sha256sums=('ca31afee32e1508cff4034e258060ce2c81a3b1c49e77da60fdb61f0e7a73c22')
b2sums=('6453e5b24be17ed10ab2c9567cac273af9941f94850388b4ef61e2114e1e1f6fd5e6fd63306107c55df068d9b4f784c6c282d8f8fba7d4b772272f6c9fa39bee')

build() {
  cd $_name-$pkgver
  python -m build --wheel --skip-dependency-check --no-isolation
}

check() {
  cd $_name-$pkgver
  pytest
}

package() {
  cd $_name-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl

  # Symlink license file
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "$pkgdir"/usr/share/licenses/$pkgname
  ln -s "$site_packages"/$_name-$pkgver.dist-info/LICENSE \
    "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
