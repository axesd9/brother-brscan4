# Maintainer: Chanathip Srithanrat <axesd9@gmail.com>

pkgname=brother-brscan4
pkgver=0.4.5_1
pkgrel=1
pkgdesc='Brother scanner drivers'
arch=('x86_64')
url='http://support.brother.com/g/s/id/linux/en/'
license=('custom:brother')
depends=('libusb-compat'
         'sane')
install="$pkgname.install"
source=("http://download.brother.com/welcome/dlf006645/${pkgname#brother-}-${pkgver/_/-}.amd64.deb"
        "http://support.brother.com/g/s/agreement/English_lpr/agree.html"
        "mk-udev-rules")
md5sums=('5ad9f6a45b9cb154c8f158b6ff8ce6cd'
         '5a4a3172f6278922062aa6e1f43b0d92'
         '46b8665634ad8692b3ad36883fefac0b')

prepare() {
    bsdtar xf data.tar.gz
    mv usr/lib64 usr/lib
    ln -sf libsane-brother4.so.1.0.7 usr/lib/sane/libsane-brother4.so.1
    ln -sf libsane-brother4.so.1 usr/lib/sane/libsane-brother4.so
    mkdir -p usr/lib/udev/rules.d
    ./mk-udev-rules opt/brother/scanner/brscan4/{Brsane4.ini,models4/*.ini} > usr/lib/udev/rules.d/40-${pkgname#brother-}.rules
}

package() {
    cp -r etc $pkgdir
    cp -r opt $pkgdir
    cp -r usr $pkgdir
    install -Dm644 agree.html $pkgdir/usr/share/licenses/$pkgname/LICENSE.html
}
