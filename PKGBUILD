# Maintainer: Rudra Saraswat <rs2009@ubuntu.com>

pkgname='blendos-first-setup-git'
pkgver=r7.cb832f7
pkgrel=1
pkgdesc="A first setup app designed for blendOS"
arch=('x86_64' 'i686')
url="https://github.com/blend-os/blendos-first-setup"
license=('GPL3')
depends=("electron")
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
makedepends=("electron" 'git' 'npm')
source=('first-setup::git+file://[BASE_ASSEMBLE_PATH]/projects/blendos-first-setup'
        'blendos-first-setup')
sha256sums=('SKIP'
            'f7648e90ded1e1d0176f0f6b57a070b0c540981f9f6eb00a5cb27c8fe3b41b1c')

pkgver() {
    cd "${srcdir}/first-setup"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    cd "${srcdir}/first-setup"
    npm config set cache "${srcdir}/npm-cache"
    npm install
}

build() {
    cd "${srcdir}/first-setup"
    npm config set cache "${srcdir}/npm-cache"
    export NODE_ENV=production
    electronDist="/usr/lib/electron"
    electronVer="$(sed s/^v// /usr/lib/electron/version)"
    npm run icons
    npm run pack -- -c.electronDist=${electronDist} \
        -c.electronVersion=${electronVer} --publish never
}

package() {
    cd "${srcdir}/first-setup"

    local _arch
    case ${CARCH} in
    i686)
        _arch=linux-ia32-unpacked
        ;;
    x86_64)
        _arch=linux-unpacked
        ;;
    *)
        _arch=linux-${CARCH}-unpacked
        ;;
    esac

    install -Dm644 "dist/${_arch}/resources/app.asar" \
        "$pkgdir/usr/lib/${pkgname%-git}/${pkgname%-git}.asar"

    for icon_size in 16 24 32 48 64 128 256 512; do
        install -Dm644 "build/icons/png/${icon_size}x${icon_size}.png" \
            "${pkgdir}/usr/share/icons/hicolor/${icon_size}x${icon_size}/apps/${pkgname%-git}.png"
    done

    install -Dm755 "${srcdir}/first-setup/${pkgname%-git}-autostart.desktop" -t \
        "${pkgdir}"/etc/xdg/autostart/
     install -Dm755 "${srcdir}"/first-setup/scripts/* -t "${pkgdir}"/usr/bin/
    install -Dm755 "${srcdir}/${pkgname%-git}" -t "${pkgdir}"/usr/bin/
}
