# Maintainer: Stefan Tatschner <stefan@sevenbyte.org>

pkgname=pynote-git
_pkgname=pynote
pkgver=1.0.0.r21.g84620a3
pkgrel=1
pkgdesc="Manage notes on the commandline"
arch=('any')
url="https://github.com/rumpelsepp/pynote"
license=('MIT')
provides=('pynote')
depends=('python' 'python-plaintable' 'python-click' 'python-babel' 'python-xdg')
optdepends=('python-pygments: synthax highlighting support')
makedepends=('python-sphinx' 'python-setuptools')
conflicts=('pynote-docs' 'pynote' 'pynote-docs-git')
source=("${_pkgname}::git+https://github.com/rumpelsepp/${_pkgname}.git")
makedepends=('git' 'python-setuptools' 'python-sphinx')
md5sums=('SKIP')

pkgver() {
  cd "${srcdir}/${_pkgname}"
  git describe --long | sed -E 's/([^-]*-g)/r\1/;s/-/./g'
  #printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
    cd "${srcdir}/${_pkgname}/docs"
    make man
    make text
}

package() {
    cd "${srcdir}/${_pkgname}"

    mkdir -p ${pkgdir}/usr/share/man/man1/
    mkdir -p ${pkgdir}/usr/share/man/man5/
    mkdir -p ${pkgdir}/usr/share/doc/pynote/

    cp -ra "docs/_build/man/note.1" "${pkgdir}/usr/share/man/man1/note.1"
    cp -ra "docs/_build/man/noterc.5" "${pkgdir}/usr/share/man/man5/noterc.5"
    cp -ra docs/_build/text/* "${pkgdir}/usr/share/doc/pynote/"

    python setup.py install --prefix=/usr --root="${pkgdir}" --optimize=1
}

