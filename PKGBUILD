# Maintainer: Daniel Bershatsky <bepshatsky@yandex.ru>
pkgname=python-dm-tree
_pkgname=${pkgname#python-}
pkgver=0.1.8
pkgrel=1
pkgdesc="A library for working with nested data structures"
arch=('any')
url="https://github.com/deepmind/tree"
license=('Apache')
groups=('deepmind' 'jax')
depends=()
makedepends=('cmake' 'git' 'make' 'python' 'python-build' 'python-installer'
             'python-setuptools')
optdepends=('python-wrapt: Prefered way for monkey patching')
source=("$_pkgname-$pkgver.tar.gz::https://github.com/deepmind/tree/archive/refs/tags/$pkgver.tar.gz")
sha256sums=('5139f26b0995514978fc214d20c8302d95c35ce58e5e1adc3278b159d39f6a52')

prepare() {
    # See https://github.com/deepmind/tree/issues/101 for details.
    export CMAKE_GENERATOR="Unix Makefiles"
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
