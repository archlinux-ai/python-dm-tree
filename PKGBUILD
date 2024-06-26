# Maintainer: Daniel Bershatsky <bepshatsky@yandex.ru>
pkgname=python-dm-tree
_pkgname=${pkgname#python-}
pkgver=0.1.8
pkgrel=3
pkgdesc="A library for working with nested data structures"
arch=('any')
url="https://github.com/google-deepmind/tree"
license=('Apache')
groups=('deepmind' 'jax')
depends=('python')
makedepends=('abseil-cpp' 'cmake' 'pybind11' 'python-build' 'python-installer'
             'python-setuptools' 'python-wheel')
optdepends=('python-wrapt: Prefered way for monkey patching')
source=("$_pkgname-$pkgver.tar.gz::https://github.com/deepmind/tree/archive/refs/tags/$pkgver.tar.gz"
        'dm-tree.patch')
sha256sums=('5139f26b0995514978fc214d20c8302d95c35ce58e5e1adc3278b159d39f6a52'
            'SKIP')

prepare() {
    # See https://github.com/deepmind/tree/issues/101 for details.
    export CMAKE_GENERATOR="Unix Makefiles"
    cd tree-$pkgver
    patch -p1 -i ../dm-tree.patch
}

build() {
    cd "tree-$pkgver"
    python -m build -n -w
}

package() {
    cd "tree-$pkgver"
    python -m installer \
        --compile-bytecode 1 \
        --destdir $pkgdir \
        dist/dm_tree-$pkgver-*_x86_64.whl
}
