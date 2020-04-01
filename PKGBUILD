# Maintainer: Aetf <aetf@unlimitedcodeworks.xyz>
# Contributor: juantascon <juantascon.aur@horlux.org>
# Contributor: Ilya Kuzmin <i.g.kuzmin.spb@gmail.com>

pkgname='hid-apple-patched-git-dkms'
_pkgname=hid-apple-patched

pkgver=20200331.f7f6560
pkgrel=1

url="https://github.com/free5lot/hid-apple-patched"
arch=('any')
license=('GPL2')
pkgdesc="Allows to swap the Fn key and left Control key on Macbook Pro and Apple keyboards in GNU/Linux (DKMS)"

depends=('dkms')
makedepends=('git')

install=hid-apple-patched-dkms.install
backup=(etc/modprobe.d/hid_apple.conf)

source=("git+https://github.com/free5lot/$_pkgname#branch=master"
        "hid-apple-patched.conf"
        "hid_apple.conf"
        "dkms.conf"
        "90-mkinitcpio-install-apple-hid.hook")

sha256sums=('SKIP'
            '4b94f1f55febddad5ff60a8918487b883ceadd4e6c3fb280e98e4e235cd09663'
            '2a493d3973b80b815779643b2c1039f52c05e2e9a65cebd00b2a1da105630cbb'
            '5d2457728a93e73a96f2ca88f66455859363f083097ad20e661bdc12dc44a9ba'
            '310e972301cca149b13e76de62409842e0ec4002404b06c73a8977a82f1c6ccc')

pkgver() {
  cd "$srcdir"/"$_pkgname"
  git log -1 --format=%cd.%h --date=short|tr -d -
}

package() {

  ## Copy sources
  install -dm755 "${pkgdir}"/usr/src/${_pkgname}-${pkgver}/
  install -Dm644 dkms.conf "${pkgdir}"/usr/src/${_pkgname}-${pkgver}/
  install -Dm644 ${_pkgname}/{hid-apple.c,hid-ids.h,Makefile} "${pkgdir}"/usr/src/${_pkgname}-${pkgver}/

  sed -e "s/@PKGNAME@/${_pkgname}/" \
      -e "s/@PKGVER@/${pkgver}/" \
      -i "${pkgdir}"/usr/src/${_pkgname}-${pkgver}/dkms.conf

  install -Dm644 hid_apple.conf "${pkgdir}"/etc/modprobe.d/hid_apple.conf
  install -Dm644 hid-apple-patched.conf "$pkgdir"/etc/depmod.d/hid-apple-patched.conf

  install -Dm644 90-mkinitcpio-install-apple-hid.hook "$pkgdir"/usr/share/libalpm/hooks/90-mkinitcpio-install-apple-hid.hook
}
