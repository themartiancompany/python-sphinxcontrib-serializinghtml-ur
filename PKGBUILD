# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

_name=sphinxcontrib_serializinghtml
pkgname=python-sphinxcontrib-serializinghtml
pkgver=1.1.8
pkgrel=1
pkgdesc='Sphinx extension which outputs "serialized" HTML files (json and pickle)'
arch=('any')
url=https://github.com/sphinx-doc/sphinxcontrib-serializinghtml
license=('BSD')
makedepends=('python-build' 'python-flit-core' 'python-installer')
checkdepends=('python-pytest' 'python-sphinx')
source=("https://files.pythonhosted.org/packages/source/${_name::1}/$_name/$_name-$pkgver.tar.gz")
sha256sums=('aaf3026335146e688fd209b72320314b1b278320cf232e3cda198f873838511a')
b2sums=('b88b5386434b02f18726a84ab600fbd8cebd0a9b732b95fed566b40a75b026c70723eb85d9a3655af57e5476623cd3d0d3cf87596d656f0a7329bfb3ae7f4eac')

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
