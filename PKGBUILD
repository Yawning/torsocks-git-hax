# Maintainer: skydrome <skydrome@i2pmail.org>
# Contributor: skydrome <skydrome@i2pmail.org>

# Modifications: Yawning Angel <yawning@torproject.org>
#
# WARNING: The extra patches applied are all considered EXPERIMENTAL, and bad
# things may happen to security or anonymity if used.
#
#  * bug15584 - Fix the SIGSEGV encountered with certain C++ apps.

pkgname=torsocks-git-hax
pkgver=2.0.0.27.gbb972f4
epoch=1
pkgrel=1
pkgdesc='Torsocks allows you to use most socks-friendly applications in a safe way with Tor.'
url='https://gitweb.torproject.org/torsocks.git'
license=('GPL2')
arch=('i686' 'x86_64')
depends=('tor')
conflicts=('torsocks' 'tsocks' 'torsocks-git')
provides=('torsocks')
options=(!strip)

source=("git+https://git.torproject.org/torsocks.git"
        'bug15584.patch')
sha256sums=('SKIP'
            '536acb63f5d6404ae21735b7ba161a783b8a88963169a62d3e82f85b9682134b')

pkgver () {
    cd "$srcdir/torsocks"
    git describe |sed 's/^v//;s/-/./g'
}

prepare() {
    cd "$srcdir/torsocks"
    export GIT_COMMITTER_NAME="nobody"
    export GIT_COMMITTER_EMAIL="nobody@localhost"
    git am "$srcdir/bug15584.patch"
    ./autogen.sh
}

build() {
    cd "$srcdir/torsocks"
    ./configure \
        --prefix=/usr \
        --sysconfdir=/etc \
        --datadir=/usr/share/torsocks \
        --docdir=/usr/share/torsocks
    make
}

package() {
    cd "$srcdir/torsocks"
    make DESTDIR="$pkgdir" install
    install -Dm644 "gpl-2.0.txt"  "$pkgdir/usr/share/licenses/torsocks/LICENSE"
    #chown -R tor:tor etc/tor &> /dev/null
}
