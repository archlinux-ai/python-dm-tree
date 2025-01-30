# Maintainer: Daniel Bershatsky <bepshatsky@yandex.ru>
pkgname=python-dm-tree
_pkgname=${pkgname#python-}
pkgver=0.1.9
pkgrel=1
pkgdesc="A library for working with nested data structures"
arch=('any')
url="https://github.com/google-deepmind/tree"
license=('Apache')
groups=('deepmind' 'jax')
depends=('python-absl' 'python-attrs' 'python-numpy' 'python-wrapt')
makedepends=('cmake' 'pybind11' 'python-build' 'python-installer'
             'python-setuptools' 'python-wheel')
checkdepends=('python-pytest')
source=("$_pkgname-$pkgver.tar.gz::https://github.com/deepmind/tree/archive/refs/tags/$pkgver.tar.gz"
        'dm-tree.diff')
sha256sums=('d736ec355daf39c93633373a160120cdd45717e6717d105efed722d2cd2cfcc9'
            'SKIP')

prepare() {
    cd "tree-$pkgver"
    patch -p1 -i../dm-tree.diff
}

build() {
    cd "tree-$pkgver"
    python -m build -nw
}

check() {
    cd "tree-$pkgver"
    find build -type f -name '_tree.*.so' -exec ln -sf ../{} tree \;
    pytest tree
}

package() {
    cd "tree-$pkgver"
    python -m installer --compile-bytecode=1 --destdir=$pkgdir \
        dist/dm_tree-$pkgver-*_x86_64.whl
}
