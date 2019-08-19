# Maintainer: Hanspeter Portner <ventosus at airpost dot net>
# Fixes: Brian Bidulock <bidulock at openss7 dot org>
 
pkgname=linuxptp
pkgver=2.0
pkgrel=1
pkgdesc='An implementation of the Precision Time Protocol (PTP) according to IEEE standard 1588 for Linux.'
arch=('i686' 'x86_64' 'armv7h' 'aarch64')
url='http://linuxptp.sourceforge.net/'
license=('GPL')
depends=('glibc')
makedepends=()
source=("https://sourceforge.net/projects/${pkgname}/files/${pkgname}-${pkgver}.tgz/download"
        "phc2sys.service"
        "ptp4l.service")
sha256sums=('0a24d9401e87d4af023d201e234d91127d82c350daad93432106284aa9459c7d'
            '66d960e1507c10b6a26346cef1f92658f62e88595138be6b7542c3640d5e712b'
            'bc6b4eac0bd1ae05cf19e6534c152444a0a27c45f57731adfb01ad6053b4289e')
 
build() {
  cd ${pkgname}-${pkgver}
  make EXTRA_CFLAGS="$CFLAGS"
}
 
package() {
  cd ${pkgname}-${pkgver}
  make prefix="${pkgdir}/usr" sbindir='$(prefix)/bin' mandir='$(prefix)/share/man' man8dir='$(mandir)/man8' install
  mkdir -p "${pkgdir}/etc/linuxptp"
  for cfg in configs/*.cfg; do
    install -Dm0644 ${cfg} "${pkgdir}/etc/linuxptp/"
  done
  install -Dm0644 "${srcdir}/phc2sys.service" "${pkgdir}/usr/lib/systemd/system/phc2sys.service"
  install -Dm0644 "${srcdir}/ptp4l.service" "${pkgdir}/usr/lib/systemd/system/ptp4l.service"
}
