pkgname='libevhtp'
pkgver=1.2.0
pkgrel=1
pkgdesc="Libevhtp was created as a replacement API for Libevent's current HTTP API."
arch=('i686' 'x86_64')
url="https://github.com/haiwen/libevhtp"
license=('BSD')
depends=(
    'openssl'
    'libevent'
    'oniguruma'
)
makedepends=('cmake')
provides=('libevhtp')
conflicts=('libevhtp')

source=(
)

sha256sums=(
)

build () {
    [[ -d "$srcdir/$pkgname-$pkgver"  ]] && rm -rf "$srcdir/$pkgname-$pkgver"
    git clone https://github.com/haiwen/libevhtp.git "$srcdir/$pkgname-$pkgver"
    cd "$srcdir/$pkgname-$pkgver"
    # Version 1.2.0 needs a patch: #include <signal.h>
    # In the current master branch this patch is not necessary anymore
    # so we simply checkout the master master branch and mark it as v 1.2.0 ;)
    # As I see it, this library never gets updated anymore
    git checkout master
    
    # This piece of crap can not be build with SSL enabled! At least not on ARCH Linux
    # It is old and incompatible with current versions. I don't understand why they still use it!
    cmake -DCMAKE_INSTALL_PREFIX=/usr -DEVHTP_DISABLE_SSL=ON -DEVHTP_BUILD_SHARED=ON ./
    make
}

package () {
    cd "$srcdir/$pkgname-$pkgver"
    make DESTDIR="$pkgdir" install
    rm -fv ${pkgdir}/usr/include/onigposix.h
    install -Dm644 LICENSE "${pkgdir}"/usr/share/licenses/${pkgname}/LICENSE
}
