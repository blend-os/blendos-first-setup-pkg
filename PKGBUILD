pkgname=blendos-first-setup
pkgver=1.0
pkgrel=1
pkgdesc='First Setup for blendOS'
url='https://github.com/blend-os/blendos-first-setup'
arch=('any')
license=('GPL-3.0')
source=("git+${url}.git")
sha256sums=('SKIP')

package() {
	mkdir -p "$pkgdir"/usr/lib/blendos-first-setup; cp "$srcdir"/blendos-first-setup/blendos-first-setup "$pkgdir"/usr/lib/blendos-first-setup
	cp -r "$srcdir"/blendos-first-setup/slides "$pkgdir"/usr/lib/blendos-first-setup
	mkdir -p "$pkgdir"/etc/xdg/autostart/; cp "$srcdir"/blendos-first-setup/blendos-first-setup-autostart.desktop "$pkgdir"/etc/xdg/autostart/
}
