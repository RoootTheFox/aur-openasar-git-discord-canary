# Maintainer: Kamack38 <kamack38.biznes@gmail.com>
_pkgname='openasar'
pkgname="${_pkgname}-git"
pkgver=r809.a8b0739
pkgrel=1
pkgdesc="Open-source alternative of Discord desktop's app.asar"
arch=('i686' 'x86_64')
url="https://github.com/GooseMod/OpenAsar"
license=('MIT')
depends=('unzip')
makedepends=('git' 'asar' 'nodejs')
optdepends=('discord-canary')
provides=("${_pkgname}")
conflicts=("${_pkgname}")
source=("git+${url}.git" "post-upgrade-discord-canary" "openasar-git-discord-upgrade.hook" "pre-remove-discord-canary" "openasar-git-discord-remove.hook")
sha1sums=('SKIP'
          '03ec1b9a69ff26f37dc7d0925410635b53bbfad7'
	  '2d77642e2349468a38b91b1f5ef58e4359e24bab'
	  '99664e9a0b07f43052cb75d5ccdb8b5123134fbc'
	  'ea36b446b5daae3f38f1ad66f9fe1e6ce51b351e'
install="$pkgname.install"

pkgver() {
    cd "${srcdir}/OpenAsar"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
    install -Dm755 "${srcdir}/post-upgrade-discord-canary" -t "${pkgdir}/usr/share/libalpm/scripts/"
    install -Dm755 "${srcdir}/pre-remove-discord-canary" -t "${pkgdir}/usr/share/libalpm/scripts/"
    install -Dm644 "${srcdir}/openasar-git-discord-remove.hook" -t "${pkgdir}/usr/share/libalpm/hooks/"
    install -Dm644 "${srcdir}/openasar-git-discord-upgrade.hook" -t "${pkgdir}/usr/share/libalpm/hooks/"
    cd "${srcdir}/OpenAsar"
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    sed -i -e "s/nightly/nightly-$(git rev-parse HEAD | cut -c 1-7)/" src/index.js
    node scripts/strip.js
    asar pack src app.asar
    install -Dm 644 app.asar "${pkgdir}/opt/${pkgname}/app.asar"
}
