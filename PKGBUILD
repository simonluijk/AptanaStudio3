# Contributor: Bruno Galeotti <bravox87 at gmail dot org>
# Maintainer: Jorge Pizarro Callejas <jpizarro at inf dot utfsm dot cl>
# Upgrade to 3.0.1: Simon Luijk <simon dot luijk gmail dot com>
pkgname=aptana-studio
_pkgname=aptana
pkgver=3.0.1
pkgrel=1
pkgdesc="The professional, open source development tool for the open web."
arch=("i686" "x86_64")
url="http://www.aptana.com/"
license=("GPLv3")
depends=("gtk2" "jre" "unzip" "xulrunner")
options=(!strip)
replaces=("aptana")
conflicts=("aptana")

if [ "$CARCH" = "i686" ]; then
    source=("http://download.aptana.com/studio3/standalone/$pkgver/linux/Aptana_Studio_3_Setup_Linux_x86_$pkgver.zip"
	    "aptana.sh"
	    "aptana.desktop"
	    "aptana-execfiles.txt")
    md5sums=("564ea0d4f9870651d996b59c8c86d8e2"
        "6b7b28fd865cdaffb66ef5f2a3e175d3"
        "e297d32ab375b84eaaabfca7bc012752"
        "d8bb2d16f20015e7da175d5e200783ee")
    noextract=("Aptana_Studio_3_Setup_Linux_x86_$pkgver.zip")
    _zipname="Aptana_Studio_3_Setup_Linux_x86_$pkgver.zip"
elif [ "$CARCH" = "x86_64" ]; then
    source=("http://download.aptana.com/studio3/standalone/$pkgver/linux/Aptana_Studio_3_Setup_Linux_x86_64_$pkgver.zip"
	    "aptana.sh"
	    "aptana.desktop"
	    "aptana-execfiles.txt")
    md5sums=("2fb8acd1cf9e7b86fce6ee72c46d68a2"
        "6b7b28fd865cdaffb66ef5f2a3e175d3"
        "e297d32ab375b84eaaabfca7bc012752"
        "d8bb2d16f20015e7da175d5e200783ee")
    noextract=("Aptana_Studio_3_Setup_Linux_x86_64_$pkgver.zip")
    _zipname="Aptana_Studio_3_Setup_Linux_x86_64_$pkgver.zip"
fi

build() {
    unzip $_zipname

    local _instpath="/usr/share"
    local _file="none"

    cd "$srcdir" || return 1
    mv "$srcdir/Aptana Studio ${pkgver%*.*.*}" "$srcdir/$_pkgname" || return 1

    # Install Dirs
    find "$_pkgname" -type d -exec install -d "{}" "$pkgdir/$_instpath/{}" \; || return 1

    # Install Files
    install -m755 -d "$pkgdir/$_instpath" || return 1
    find "$_pkgname" -type f \
	    $(cat "$startdir/$_pkgname-execfiles.txt" | sed -e "s/^/-not -path /" | sed -e "N;s:\n: :g") \
	    -exec install -Dm644 "{}" "$pkgdir/$_instpath/{}" \; || return 1

    # Install Executables
    for _file in $(cat "$startdir/$_pkgname-execfiles.txt"); do
	    install -Dm755 "$_file" "$pkgdir/$_instpath/$_file" || return 1
    done || return 1

    # install misc
    install -d "$pkgdir/usr/bin" "$pkgdir/$_instpath"/{applications,pixmaps} || return 1
    install -m755 "$startdir/$_pkgname.sh" "$pkgdir/usr/bin/$_pkgname" || return 1
    install -m644 "$startdir/aptana.desktop" "$pkgdir/$_instpath/applications/" || return 1
    ln -s "$_instpath/$_pkgname/icon.xpm" "$pkgdir/$_instpath/pixmaps/$_pkgname.xpm" || return 1
}
