pkgname=SmartGuitarAmp
pkgver=1.3
pkgrel=1
pkgdesc="Guitar plugin made with JUCE that uses neural network models to emulate real world hardware."
arch=('x86_64')
url="https://guitarml.com/"
license=('Apache')
conflicts=('smartguitaramp')
provides=('smartguitaramp')
source=("git+https://github.com/GuitarML/SmartGuitarAmp.git")
sha256sums=('SKIP')

prepare() {
    cd "$srcdir/$pkgname"
    git submodule init
    git submodule update --recursive
}

build() {
    cmake -B build -S "$srcdir/$pkgname" \
        -DCMAKE_BUILD_TYPE='lib' \
        -DCMAKE_INSTALL_PREFIX='/usr' \
        -Wno-dev
    cmake --build build --config Release
}

package() {
    cd "$srcdir"

    install -d "$pkgdir/usr/lib/lv2"
	cp -rfd build/SmartAmp_artefacts/lib/LV2/SmartAmp.lv2 "$pkgdir/usr/lib/lv2/"

	install -d "$pkgdir/usr/lib/vst3"
	cp -rfd build/SmartAmp_artefacts/lib/VST3/SmartAmp.vst3 "$pkgdir/usr/lib/vst3/"

	install -D -m644 $pkgname/LICENSE -t "$pkgdir/usr/share/licenses/$pkgname/"
}
