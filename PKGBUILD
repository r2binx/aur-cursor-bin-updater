# Maintainer: Your Name <your.email@example.com>

pkgname=cursor-bin
pkgver=0.42.5
pkgrel=1
pkgdesc="Cursor App - AI-first coding environment"
arch=('x86_64')
url="https://www.cursor.com/"
license=('custom:Proprietary')  # Replace with the correct license if known
depends=('fuse2')
options=(!strip)
source_x86_64=("https://download.todesktop.com/230313mzl4w4u92/cursor-0.42.5-build-24111460bf2loz1-x86_64.AppImage" "cursor.png")
noextract=("$(basename ${source_x86_64[0]})")
sha512sums_x86_64=('9da6e4d854daa252abca7707b43d754c26a28ea2170ed34dfcfaab1bfb7d4f6930cad23ac53ea6fab8f59f8638e590d853e21f8d871ce0b02bf9fe0cca7e1e29'
                   'f948c5718c2df7fe2cae0cbcd95fd3010ecabe77c699209d4af5438215daecd74b08e03d18d07a26112bcc5a80958105fda724768394c838d08465fce5f473e7')
package() {
    install -Dm755 "${srcdir}/$(basename ${source_x86_64[0]})" "${pkgdir}/opt/${pkgname}/${pkgname}.AppImage"

    # Symlink executable to be called 'cursor'
    mkdir -p "${pkgdir}/usr/bin"
    ln -s "/opt/${pkgname}/${pkgname}.AppImage" "${pkgdir}/usr/bin/cursor"

    # Install the icon
    install -Dm644 "${srcdir}/cursor.png" "${pkgdir}/usr/share/icons/hicolor/512x512/apps/cursor.png"

    # Create a .desktop Entry
    mkdir -p "${pkgdir}/usr/share/applications"
    cat <<EOF > "${pkgdir}/usr/share/applications/cursor-cursor.desktop"
[Desktop Entry]
Name=Cursor
Exec=/usr/bin/cursor --no-sandbox %U
Terminal=false
Type=Application
Icon=cursor
StartupWMClass=cursor-url-handler
X-AppImage-Version=${pkgver}
MimeType=x-scheme-handler/cursor;
Categories=Utility;TextEditor;Development;IDE
EOF
}

post_install() {
    update-desktop-database -q
    xdg-icon-resource forceupdate
}
