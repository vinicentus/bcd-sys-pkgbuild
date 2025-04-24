# Maintainer: Vincent Långström <vincent.langstrom@gmail.com>
pkgname=bcd-sys
pkgver=v2.0
pkgrel=1
pkgdesc='BASH script to set up Windows Boot Manager from Linux/macOS, like bcdboot.'
arch=('any')
license=('GPL-3.0-or-later')
url='https://github.com/jpz4085/BCD-SYS'
# TODO: idk if attr should be listed, since it is a dependency of coreutils which is a dep of base...
depends=('hivex' 'readpe' 'attr' 'fatattr' 'xxd')
optdepends=('qemu-base: VHDX Support'
            'ms-sys: Legacy BIOS support')
makedepends=('git' 'perl')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/${pkgver}.tar.gz")
b2sums=('feb48366035f9afb0b38440019edfb03978c2998b1dcdecb7ab2200e117a62c8926b55a59139e6983c4245018c26087a8288be9fb294546a4ed92af9de52540c')

package() {
  local platform="Linux"
  local bindir="/usr/bin"
  local resdir="/usr/share/BCD-SYS"

  mkdir -p "$pkgdir/$bindir"
  mkdir -p "$pkgdir/$resdir"
  mkdir "$pkgdir/$resdir/Resources"

  cd "$srcdir/BCD-SYS-2.0"

  install "$platform/bcd-sys.sh" "$pkgdir/$bindir/bcd-sys"
  install "$platform/recovery.sh" "$pkgdir/$resdir"
  install "$platform/update_device.sh" "$pkgdir/$resdir"
  install "$platform/wbmfwvar.sh" "$pkgdir/$resdir"
  install "$platform/winload.sh" "$pkgdir/$resdir"
  install Resources/attach-vhdx.sh "$pkgdir/$bindir/attach-vhdx"
  install Resources/detach-vhdx.sh "$pkgdir/$bindir/detach-vhdx"
  cp Resources/*.txt "$pkgdir/$resdir/Resources"
  cp -r Templates "$pkgdir/$resdir"
  # TODO: use sed instead of perl so that we can get rid of a makedep
  perl -i -pe"s|resdir=\".\"|resdir=\"$resdir\"|" "$pkgdir/$bindir/bcd-sys"
  perl -i -pe"s|tmpdir=\".\"|tmpdir=\"/tmp\"|" "$pkgdir/$bindir/bcd-sys"
  perl -i -pe"s|resdir=\".\"|resdir=\"$resdir\"|" "$pkgdir/$resdir/recovery.sh"
  perl -i -pe"s|resdir=\".\"|resdir=\"$resdir\"|" "$pkgdir/$resdir/winload.sh"
}
