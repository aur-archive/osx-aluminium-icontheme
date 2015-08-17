# Maintainer: Limao Luo <luolimao+AUR@gmail.com>

pkgname=osx-aluminium-icontheme
pkgver=1.2
pkgrel=8
pkgdesc="Mac OSX Aluminium icon theme"
arch=(any)
url=http://3rik.free.fr/Linux/Themes
license=(unknown)
source=($url/Xfce/OSX_Aluminium-$pkgver.tar.bz2
    index-theme.patch)
sha256sums=('595b23f8354fe1e39d533735723ef4ca582fbb39fff1c43adfe3fc9fcc259bdf'
    'ae86e10c9bec83743271be50f009299a58e6bf4619514b76e950ec9c53c61e68')
sha512sums=('7bc62e396e3f0dfd40c758b4bfd8762637f9509fbf1e0679acbe3383a896c006384f2fb728ee308a1e0b506884ddbeedd5301a01d200de9e1465155698345a43'
    '00333360f40e7190cf816096ac6a760ca25a66ae5c4221e94786a44e69727049599e8a896811da660b72465172a563d6c3b5ef8d45357a5992192448bdc91706')

prepare() {
    patch -p1 -i index-theme.patch
}

build() {
    find -type f -exec chmod 644 '{}' \;
    cd OSX_Aluminium/128x128/apps/

    # adds in extra missing links
    install -d ../categories/
    _targets=(gnome-session-hibernate.png
        gnome-session-suspend.png
        gnome-session-reboot.png
        gnome-session-halt.png
        gnome-network-preferences.png
        gnome-monitor.png
        gnome-help.png
        gnometris.png
        system-config-securitylevel.png
        abiword.png
        kmail.png)
    _links=(xfsm-hibernate.png
        xfsm-suspend.png
        xfsm-reboot.png
        system-shutdown.png
        preferences-system-network.png
        xfce4-taskmanager.png
        ../categories/gtk-help.png
        gnome-quadrapassel.png
        system-log-out.png
        abiword_48.png
        exo-mail-reader.png)
    # symlinks the links to the targets
    for i in $(seq 0 $(expr ${#_targets[*]} - 1)); do
        ln -sf ${_targets[$i]} ${_links[$i]}
    done
    for i in xfsm*; do
        ln -sf $(readlink $i) xfpm${i:4}
    done
    ln -sf $(readlink ../categories/gtk-help.png) ../gtk/gtk-help.png

    # switches reboot and grsync icons
    mv gnome-session-reboot.png TMPFILE
    mv grsync.png gnome-session-reboot.png
    mv TMPFILE grsync.png
}

package() {
    install -d "$pkgdir"/usr/share/icons/
    cp -r OSX_Aluminium/ "$pkgdir"/usr/share/icons/
}
