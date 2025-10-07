# Maintainer: Colin Adler <colin@coder.com>
# Maintainer: Asher <ash@coder.com>
# Maintainer: cdrci <joe+cdrci@coder.com>
# Contributor: Joe Previte <joe@coder.com>
# Contributor: Teffen Ellis <teffen@coder.com>
# Contributor: Anmol <anmol@coder.com>

pkgname=code-server
pkgver=4.104.3
pkgrel=1
pkgdesc="VS Code in the browser"
arch=("x86_64" "aarch64")
url="https://github.com/coder/code-server"
license=(MIT)
depends=(glibc)
source=(
  "$pkgname-$pkgver-user.service::https://raw.githubusercontent.com/cdr/code-server/v$pkgver/ci/build/code-server-user.service"
  "$pkgname-$pkgver@.service::https://raw.githubusercontent.com/cdr/code-server/v$pkgver/ci/build/code-server@.service"
)
release_name="code-server-${pkgver}-linux"
source_x86_64=(
  "${url}/releases/download/v$pkgver/$release_name-amd64.tar.gz"
)
source_aarch64=(
  "${url}/releases/download/v$pkgver/$release_name-arm64.tar.gz"
)
sha512sums=('7040df09c7404a56dbbb32e09d04ead3b622773520feae19c6710656cef46ca5d79b1972bfebb931e309e495d041b9938cd6a51c39fc0f8f6133dfe711be9280'
            'ab8e679c05f6184f163dccf0651e8c1fac22a29ae583148f8c93b6930ece27cdff45a48b425e8b15b8c8ce749015680a3ae8225b7e8037979ff3d228f396f629')
sha512sums_x86_64=('4d5d2b18ebccf31b2683a56f28870f474cb7855269f5522264c75e3a6f21c90776541ec741983cf53547120c6177de598a1b7efd66a9929725c0802f398f9a41')
sha512sums_aarch64=('dc515ab66bfee3e613f9d60d3693b3f3ddaf8a622d9edc63a46d6fa51f3f1c06a6f7a78ced9fdb9ad9368a76a0e015d0c02920af1b8cbf023b415f4039f9ad1a')
package() {
  if [[ ${CARCH} == x86_64 ]]; then
    release_name+=-amd64
  else
    release_name+=-arm64
  fi

  mkdir -p "$pkgdir/usr/lib"
  cp -a "$release_name" "$pkgdir/usr/lib/$pkgname"

  mkdir -p "$pkgdir/usr/bin"
  ln -s "/usr/lib/$pkgname/bin/$pkgname" "$pkgdir/usr/bin/$pkgname"

  mkdir -p "$pkgdir/usr/lib/systemd/system"
  cp -aL "$pkgname-$pkgver@.service" "$pkgdir/usr/lib/systemd/system/$pkgname@.service"

  mkdir -p "$pkgdir/usr/lib/systemd/user"
  cp -aL "$pkgname-$pkgver-user.service" "$pkgdir/usr/lib/systemd/user/$pkgname.service"

  mkdir -p "$pkgdir/usr/share/licenses"
  cp -a "$release_name/LICENSE" "$pkgdir/usr/share/licenses/$pkgname"
}
