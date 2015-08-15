# Maintainer:Atilla ÖNTAŞ <tarakbumba@gmail.com>

_pkgname=enchant
pkgname=enchant-zemberek
pkgver=1.6.0
pkgrel=4
pkgdesc="A wrapper library for generic spell checking with zemberek support"
arch=('i686' 'x86_64')
url="http://www.abisource.com/enchant/"
license=('LGPL')
depends=('aspell' 'dbus-glib' 'hunspell' 'hspell' 'enchant')
makedepends=('hspell')
options=('!libtool')
provides=("enchant-zemberek=${pkgver}-${pkgrel}")
replaces=("enchant-zemberek<=${pkgver}-${pkgrel}")
conflicts=("enchant-zemberek<=${pkgver}-${pkgrel}")
source=("http://www.abisource.com/downloads/${_pkgname}/${pkgver}/${_pkgname}-${pkgver}.tar.gz")
md5sums=('de11011aff801dc61042828041fb59c7')

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  ./configure --prefix=/usr \
    --disable-static \
    --disable-ispell \
    --disable-voikko \
    --enable-zemberek \
    --with-myspell-dir=/usr/share/myspell
  make || return 1
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  #We only need zemberek library and do not wan't conflicts with enchant package,
  #so remove dirs and files other than enchant-zemberek
  rm -rf ${pkgdir}/usr/{bin,share,include,lib/pkgconfig,lib/libenchant*,}
  rm -rf ${pkgdir}/usr/lib/enchant/{libenchant_aspell.so,libenchant_hspell.so,libenchant_myspell.so}

}
