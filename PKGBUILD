# Maintainer: Roberto Nobrega <rwnobrega@gmail.com>
# Contributor: Andrew Burkett <burkett.andrew@gmail.com>
# Contributor: Daniel J Griffiths <ghost1227@archlinux.us>

pkgname=launchy-svn
pkgver=671
pkgrel=4
pkgdesc="Launchy indexes the programs in your start menu and can launch your documents, project files, folders, and bookmarks with just a few keystrokes! (SVN version)"
arch=('i686' 'x86_64')
url="http://www.launchy.net/"
license=('GPL')
depends=('qt4' 'xdg-utils')
makedepends=('gcc' 'boost' 'subversion')
source=("fix-linking.patch")
sha256sums=("6b3c553c1669c4ff363b72923847996a6fe9eecb6ea83f631c2a7eedf54a3a30")

_svnmod="launchy"
_svntrunk="https://launchy.svn.sourceforge.net/svnroot/launchy/trunk/Launchy_QT"

build() {
    cd ${srcdir}

    msg "Connecting to SVN server...."
    if [ -d ${_svnmod}/.svn ]; then
        (cd ${_svnmod} && svn up -r $pkgver)
    else
        svn co ${_svntrunk} --config-dir ./ -r $pkgver ${_svnmod}
    fi
    msg "SVN checkout done or server timeout"

    msg "Starting make..."
    cd ${_svnmod}

    # fix linking against libX11
    patch -Np1 -i ../../fix-linking.patch

    qmake-qt4 -r Launchy.pro
    make
}

package() {
    cd ${srcdir}/${_svnmod}
    make INSTALL_ROOT=${pkgdir} install
}
