# Maintainer: Douglas Chimento
pkgname=lnd-bin
_pkgname=lnd
pkgver=0.14.2_beta
_pkgver="${pkgver//_/-}"
__pkgver="${_pkgver//\./\\\.}"
pkgrel=3
pkgdesc="Lightning Network Daemon ⚡"
arch=('x86_64')
url="https://github.com/lightningnetwork/lnd"
license=('MIT')
provides=('lnd' 'lncli')
conflicts=('lnd' 'lnd-git')
backup=('etc/lnd/lnd.conf')
source=(
    "https://github.com/lightningnetwork/$_pkgname/releases/download/v$_pkgver/$_pkgname-linux-amd64-v$_pkgver.tar.gz"
    "$_pkgname-LICENSE-v$_pkgver::https://raw.githubusercontent.com/lightningnetwork/$_pkgname/v$_pkgver/LICENSE"
    "lnd.user"
    "lnd.conf"
    "lnd-chown.hook"
    "lnd@.service"
)
sha512sums=(
    '598b24c19ef8146a2d4a55106d8592c0dbbc6c6c67bb9294a4244791a87306a59a2be14cc738501fa44f3773618e376b47c74fb6b1295d31bd463889d8f10dbf'
    '9837c5d097a2838cf6dc992cc25b9e94946e401131e13e66a699077c3e2de1b89fb1de71027d46d7230464ebbad3ae8df118d459961b28995677d56fded451ca'
    SKIP
    SKIP
    SKIP
    SKIP
)

package() {
  install -Dm 755 "$srcdir/$_pkgname-linux-amd64-v$_pkgver/lncli" -t "$pkgdir/usr/bin";
  install -Dm 755 "$srcdir/$_pkgname-linux-amd64-v$_pkgver/lnd" -t "$pkgdir/usr/bin";
  install -Dm644 "${srcdir}/$_pkgname-LICENSE-v$_pkgver" -t "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

  install -m 755 -d "${pkgdir}/usr/lib/sysusers.d"
  install -m 750 -d "${pkgdir}/var/lib/lnd"
  install -m 750 -d "${pkgdir}/etc/lnd"
  
  install -m 644 "${srcdir}/lnd.user" "${pkgdir}/usr/lib/sysusers.d/${pkgname}.conf"
  install -m 640 "${srcdir}/lnd.conf" "${pkgdir}/etc/lnd/lnd.conf"
  install -Dm 644 "${srcdir}/lnd@.service" -t "${pkgdir}/usr/lib/systemd/system"

  msg2 'Installing pacman hooks...'
  install -Dm 644 "$srcdir"/*.hook -t "$pkgdir/usr/share/libalpm/hooks"
}

