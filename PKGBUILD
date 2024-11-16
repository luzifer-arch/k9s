# Maintainer: Knut Ahlers
# Contributor: Alexander F. Rødseth <xyproto@archlinux.org>
# Contributor: Morten Linderud <foxboron@archlinux.org>

pkgname=k9s
pkgver=0.32.7
pkgrel=1
pkgdesc='TUI for managing Kubernetes clusters and pods'
arch=(x86_64)
url='https://github.com/derailed/k9s'
license=(APACHE)
makedepends=(git go)
options=('!lto')
source=("git+$url#tag=v${pkgver}")
sha256sums=('3aaa31b37ae35f3be0e86fc38fd7911b88ba709444ba4a5077794eda6a536251')
options=('!lto')

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/^v//;s/-/+/g'
}

build() {
  cd $pkgname
  export CGO_LDFLAGS="${LDFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -mod=readonly -modcacherw"
  make VERSION=$pkgver build
}

check() {
  make -C $pkgname test
}

package() {
  cd $pkgname
  execs/k9s completion bash | install -Dm644 /dev/stdin "$pkgdir/usr/share/bash-completion/completions/k9s"
  execs/k9s completion zsh | install -Dm644 /dev/stdin "$pkgdir/usr/share/zsh/site-functions/_k9s"
  execs/k9s completion fish | install -Dm644 /dev/stdin "$pkgdir/usr/share/fish/vendor_completions.d/k9s.fish"
  install -Dm755 "execs/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# getver: github.com/derailed/k9s/releases
# vim: ts=2 sw=2 et:
