# Maintainer: skydrome <skydrome@i2pmail.org>
# Contributor: skydrome <skydrome@i2pmail.org>

# Modifications: Yawning Angel <yawning@torproject.org>
#
# WARNING: The extra patches applied are all considered EXPERIMENTAL, and bad
# things may happen to security or anonymity if used.
#
#  * bug13294 - Add support for gettid, getrandom, futex.
#  * bug15497 - Fix the broken getpeername implementation.
#  * bug15504 - Fix the broken getaddrinfo implementation.
#  * bug15584 - Fix the SIGSEGV encountered with certain C++ apps.

pkgname=torsocks-git-hax
pkgver=2.0.0.17.gbd6ae94
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
        'bug13294.patch'
        'bug15497.patch'
        'bug15504.patch'
        'bug15584.patch')
sha256sums=('SKIP'
            '38a77180e41e8dcd0bfaaaab9d48e557f7cda4a31ea731b3393dacdace6b64f1'
            'ebda13ac82dd002a444f188257051a2b90514b6a00eaa3f7dce04bd0a4e13fcd'
            'b875c5594365938c76d0d342604b669e519876dfd76b91d793d3a01c4abc6962'
            '69168263f994b98622b2266780dbf355e39cfab897b6f555d43da76d30064b5b')

pkgver () {
    cd "$srcdir/torsocks"
    git describe |sed 's/^v//;s/-/./g'
}

prepare() {
    cd "$srcdir/torsocks"
    git am "$srcdir/bug13294.patch"
    git am "$srcdir/bug15497.patch"
    git am "$srcdir/bug15504.patch"
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
