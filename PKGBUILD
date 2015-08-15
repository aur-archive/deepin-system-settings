# Maintainer: Xu Fasheng <fasheng.xu[AT]gmail.com>

### MERGE TO ONE PACKAGE FOR AUR
pkgname='deepin-system-settings'
pkgdesc='Utility classes for using DCM modules in Linux Deepin environment'
depends=('python2' 'polkit' 'python2-xappy' 'deepin-ui' 'deepin-gsettings' 'gnome-settings-daemon' 'python2-pexpect' 'gstreamer0.10' 'python2-psutil' 'bluez' 'obex-data-server' 'python2-deepin-lunar' 'ntp' 'xautomation' 'python2-deepin-xrandr' 'deepin-gsettings' 'python2-deepin-storm' 'libgnomekbd' 'python2-gconf' 'python2-xklavier' 'libgnomekbd' 'python2-keyring' 'python2-gudev' 'modemmanager' 'glib-networking' 'networkmanager' 'networkmanager-pptp' 'python2-pytz' 'python2-dbus' 'python2-deepin-pulseaudio' 'python2-gtop')

# pkgname=('deepin-system-settings'
#          'deepin-system-settings-module-all'
#          'deepin-system-settings-module-a11y'
#          'deepin-system-settings-module-account'
#          'deepin-system-settings-module-application-associate'
#          'deepin-system-settings-module-bluetooth'
#          'deepin-system-settings-module-date-time'
#          'deepin-system-settings-module-desktop'
#          'deepin-system-settings-module-display'
#          'deepin-system-settings-module-driver'
#          'deepin-system-settings-module-individuation'
#          'deepin-system-settings-module-keyboard'
#          'deepin-system-settings-module-mouse'
#          'deepin-system-settings-module-network'
#          'deepin-system-settings-module-power'
#          'deepin-system-settings-module-printer'
#          'deepin-system-settings-module-sound'
#          'deepin-system-settings-module-system-information'
#          'deepin-system-settings-module-touchpad'
#          'deepin-system-settings-module-tray-power'
#          'deepin-system-settings-module-mount-media')
# pkgbase=deepin-system-settings
pkgver=git20140303144502
pkgrel=1
arch=('any')
url="http://www.linuxdeepin.com/"
license=('GPL2')
# depends=('python2' 'polkit' 'python2-xappy')
makedepends=('python2-setuptools')

_fileurl=http://packages.linuxdeepin.com/deepin/pool/main/d/deepin-system-settings/deepin-system-settings_1+git20140303144502~bb2b8f57a5.tar.gz
source=("${_fileurl}")
md5sums=('7d909643b418b70a26f1e7330b76c3cb')

_filename="$(basename "${_fileurl}")"
_filename="${_filename%.tar.gz}"
_innerdir="${_filename/_/-}"

_install_copyright_and_changelog() {
    mkdir -p "${pkgdir}/usr/share/doc/${pkgname}"
    cp -f debian/copyright "${pkgdir}/usr/share/doc/${pkgname}/"
    gzip -c debian/changelog > "${pkgdir}/usr/share/doc/${pkgname}/changelog.gz"
}

# Usage: _install_desktop dest file.desktop...
_install_desktop() {
    local dest=$1; shift
    mkdir -p "${dest}"
    install -vm 0644 -t "${dest}" "$@"
}

# Usage: _install_link linkfile target
_install_link() {
    local linkfile=$1
    local target=$2
    mkdir -p "$(dirname ${linkfile})"
    ln -s "${target}" "${linkfile}"
}

# Usage: _easycp dest files...
_easycp () {
    local dest=$1; shift
    mkdir -p "${dest}"
    cp -R -t "${dest}" "$@"
}

prepare() {
    cd "${srcdir}/${_innerdir}"

    # fix python version
    find -iname "*.py" | xargs sed -i 's=\(^#! */usr/bin.*\)python=\1python2='

    sed -i 's/subprocess.Popen("python %s/subprocess.Popen("python2 %s/' \
        dss/main.py

    sed -i "s/startswith('python')/startswith('python2')/" \
        modules/sound/src/tray_sound_gui_small.py

    sed -i "s/'command': \"python /'command': \"python2 /" \
        modules/keyboard/src/keybind_all.py
    sed -i "s/'command': 'python /'command': 'python2 /" \
        modules/keyboard/src/keybind_all.py

    sed -i 's/subprocess.Popen("python %s/subprocess.Popen("python2 %s/' \
        modules/bluetooth/src/tray_bluetooth_plugin.py
}

package_deepin-system-settings() {
    depends=('deepin-ui' 'deepin-gsettings' 'deepin-system-settings-module-all')
    pkgdesc='Utility classes for using DCM modules in Linux Deepin environment'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/ app_theme
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/ image
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/ dss
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/ skin
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/ search_db
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/ locale
    _install_desktop "${pkgdir}"/usr/share/applications/ debian/deepin-system-settings.desktop
    _install_link "${pkgdir}"/usr/bin/deepin-system-settings /usr/share/deepin-system-settings/dss/main.py
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-all() {
    depends=('deepin-system-settings' 'deepin-system-settings-module-a11y' 'deepin-system-settings-module-account' 'deepin-system-settings-module-application-associate' 'deepin-system-settings-module-bluetooth' 'deepin-system-settings-module-date-time' 'deepin-system-settings-module-desktop' 'deepin-system-settings-module-display' 'deepin-system-settings-module-driver' 'deepin-system-settings-module-individuation' 'deepin-system-settings-module-keyboard' 'deepin-system-settings-module-mouse' 'deepin-system-settings-module-network' 'deepin-system-settings-module-power' 'deepin-system-settings-module-printer' 'deepin-system-settings-module-sound' 'deepin-system-settings-module-system-information' 'deepin-system-settings-module-touchpad' 'deepin-system-settings-module-mount-media' 'deepin-system-settings-module-tray-power')
    pkgdesc='Deepin system settings module for configuring system'

    cd "${srcdir}/${_innerdir}"
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-a11y() {
    depends=('deepin-system-settings')
    pkgdesc='Deepin system settings module for configuring accessibility'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/a11y
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-account() {
    depends=('deepin-system-settings' 'polkit' 'python2-pexpect' 'gstreamer0.10')
    pkgdesc='Deepin system settings module for configuring accounts'

    cd "${srcdir}/${_innerdir}"

    (
        cd modules/account/src;
        python2 setup.py install --prefix=/usr --root "${pkgdir}"
    )
    # TODO find "${_destdir}"/deepin-system-settings-module-account/usr/share/deepin-system-settings \( -name "*.c" -or -name "setup.py" -or -name "com.deepin.*"  -or -name "install_backend.sh" \) -delete

    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/account
    _easycp "${pkgdir}"/usr/share/dbus-1/system-services/ modules/account/src/com.deepin.passwdservice.service
    _easycp "${pkgdir}"/usr/share/polkit-1/actions/ modules/account/src/com.deepin.passwdservice.policy
    _easycp "${pkgdir}"/etc/dbus-1/system.d/ modules/account/src/com.deepin.passwdservice.conf
    _easycp "${pkgdir}"/usr/lib/ modules/account/src/passwdservice.py
    _easycp "${pkgdir}"/var/lib/AccountsService/icons/ modules/account/faces/*

    _install_copyright_and_changelog
}

package_deepin-system-settings-module-application-associate() {
    depends=('deepin-system-settings' 'python2-psutil')
    pkgdesc='Deepin system settings module for configuring application associate'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/application_associate
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-bluetooth() {
    depends=('deepin-system-settings' 'bluez' 'obex-data-server')
    pkgdesc='Deepin system settings module for configuring bluetooth'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/bluetooth
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-date-time() {
    depends=('deepin-system-settings' 'python2-deepin-lunar' 'ntp')
    pkgdesc='Deepin system settings module for configuring date and time'

    cd "${srcdir}/${_innerdir}"

    (
        cd modules/date_time/src
        python2 setup.py install --prefix=/usr --root "${pkgdir}"
    )
    # TODO find "${_destdir}"/deepin-system-settings-module-date-time/usr/share/deepin-system-settings \( -name "*.c" -or -name "setup.py" -or -name "com.deepin.*"  -or -name "install_backend.sh" -or -name "*.h" \) -delete

    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/date_time
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-desktop() {
    depends=('deepin-system-settings' 'xautomation')
    pkgdesc='Deepin system settings module for configuring desktop'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/desktop
    _install_copyright_and_changelog
}

# TODO
package_deepin-system-settings-module-display() {
    depends=('deepin-system-settings' 'python2-deepin-xrandr' 'deepin-gsettings')
    pkgdesc='Deepin system settings module for configuring display'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/display
    _install_copyright_and_changelog
}

# TODO
package_deepin-system-settings-module-driver() {
    depends=('deepin-system-settings')
    pkgdesc='Deepin system settings module for configuring driver'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/driver
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-individuation() {
    depends=('deepin-system-settings' 'python2-deepin-storm')
    # TODO 'python-pystorm' 'deepin-default-wallpapers'
    pkgdesc='Deepin system settings module for configuring individuation'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/individuation/ modules/individuation/data
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/individuation/ modules/individuation/locale
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/individuation/ modules/individuation/src
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/individuation/ modules/individuation/config.ini
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/individuation/ modules/individuation/__init__.py
    _install_copyright_and_changelog
}

# TODO error: (main.py:11977): GLib-GIO-ERROR **: Settings schema
# 'org.gnome.settings-daemon.plugins.key-bindings' is not installed
package_deepin-system-settings-module-keyboard() {
    depends=('deepin-system-settings' 'libgnomekbd' 'python2-gconf' 'python2-xklavier' 'libgnomekbd')
    pkgdesc='Deepin system settings module for configuring keyboard'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/keyboard
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-mount-media() {
    depends=('deepin-system-settings')
    pkgdesc='Deepin system settings module for configuring mount media'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/mount_media
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-mouse() {
    depends=('deepin-system-settings')
    pkgdesc='Deepin system settings module for configuring mouse'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/mouse
    _install_copyright_and_changelog
}

# TODO error: nmlib.nm_utils.InvalidService: 'InvalidService:org.freedesktop.ModemManager'
package_deepin-system-settings-module-network() {
    depends=('deepin-system-settings' 'python2-keyring' 'python2-gudev' 'modemmanager' 'glib-networking' 'networkmanager' 'networkmanager-pptp' 'python2-pytz')
    # TODO 'networkmanager-l2tp'
    pkgdesc='Deepin system settings module for configuring network'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/network
    _easycp "${pkgdir}"/usr/share/dbus-1/system-services/ modules/network/src/nmlib/com.deepin.network.service
    _easycp "${pkgdir}"/etc/dbus-1/system.d/ modules/network/src/nmlib/com.deepin.network.conf
    _easycp "${pkgdir}"/usr/share/polkit-1/actions/ modules/network/src/nmlib/com.deepin.network.policy
    _easycp "${pkgdir}"/usr/lib/ modules/network/src/nmlib/network_service.py
    _install_copyright_and_changelog
}

# TODO error: IOError: [Errno 2] No such file or directory: '/home/fsh/.config/powers.xml'
package_deepin-system-settings-module-power() {
    depends=('deepin-system-settings')
    pkgdesc='Deepin system settings module for configuring power manager'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/power
    _install_copyright_and_changelog
}

# TODO
package_deepin-system-settings-module-printer() {
    depends=('deepin-system-settings')
    pkgdesc='Deepin system settings module for configuring printer'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/printer
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-sound() {
    depends=('deepin-system-settings' 'python2-dbus' 'python2-deepin-pulseaudio')
    pkgdesc='Deepin system settings module for configuring sound'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/sound
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-system-information() {
    depends=('deepin-system-settings' 'python2-gtop')
    pkgdesc='Deepin system settings module for configuring system-information'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/system_information
    _install_copyright_and_changelog
}

package_deepin-system-settings-module-touchpad() {
    depends=('deepin-system-settings')
    pkgdesc='Deepin system settings module for configuring touchpad'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/touchpad
    _install_copyright_and_changelog
}

# TODO error: IOError: [Errno 2] No such file or directory: '/home/fsh/.config/powers.xml'
package_deepin-system-settings-module-tray-power() {
    depends=('deepin-system-settings')
    pkgdesc='Deepin system settings module for configuring tray power icon'

    cd "${srcdir}/${_innerdir}"
    _easycp "${pkgdir}"/usr/share/deepin-system-settings/modules/ modules/tray_power
    _install_copyright_and_changelog
}

### MERGE TO ONE PACKAGE FOR AUR
package() {
    package_deepin-system-settings
    package_deepin-system-settings-module-all
    package_deepin-system-settings-module-a11y
    package_deepin-system-settings-module-account
    package_deepin-system-settings-module-application-associate
    package_deepin-system-settings-module-bluetooth
    package_deepin-system-settings-module-date-time
    package_deepin-system-settings-module-desktop
    package_deepin-system-settings-module-display
    package_deepin-system-settings-module-driver
    package_deepin-system-settings-module-individuation
    package_deepin-system-settings-module-keyboard
    package_deepin-system-settings-module-mouse
    package_deepin-system-settings-module-network
    package_deepin-system-settings-module-power
    package_deepin-system-settings-module-printer
    package_deepin-system-settings-module-sound
    package_deepin-system-settings-module-system-information
    package_deepin-system-settings-module-touchpad
    package_deepin-system-settings-module-tray-power
    package_deepin-system-settings-module-mount-media

    # overwrite variables again, or upload to aur may be failed
    pkgname='deepin-system-settings'
    pkgdesc='Utility classes for using DCM modules in Linux Deepin environment'
    depends=('python2' 'polkit' 'python2-xappy' 'deepin-ui' 'deepin-gsettings' 'deepin-gnome-settings-daemon' 'python2-pexpect' 'gstreamer0.10' 'python2-psutil' 'bluez' 'obex-data-server' 'python2-deepin-lunar' 'ntp' 'xautomation' 'python2-deepin-xrandr' 'deepin-gsettings' 'python2-deepin-storm' 'libgnomekbd' 'python2-gconf' 'python2-xklavier' 'libgnomekbd' 'python2-keyring' 'python2-gudev' 'modemmanager' 'glib-networking' 'networkmanager' 'networkmanager-pptp' 'python2-pytz' 'python2-dbus' 'python2-deepin-pulseaudio' 'python2-gtop')
}
