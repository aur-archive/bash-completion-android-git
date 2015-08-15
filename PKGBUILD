# Contributor: Mike Redd <mredd -at- zerotuezero dot com>

pkgname=bash-completion-android-git
pkgver=20140806
pkgrel=2.5
pkgdesc='Bash completion by Matt Brubeck for android, adb, emulator, fastboot and repo'
arch=('any')
url="https://github.com/MikereDD/android-completion"
license=('MIT')
depends=('bash' 'android-sdk' 'git')
conflicts=('bash-completion-adb-git')
install=
source=("git+https://github.com/MikereDD/android-completion.git")

md5sums=('SKIP')
sha256sums=('SKIP')

_gitroot="git://github.com/MikereDD/android-completion.git"
_gitname="android-completion"
_buildir="${_gitname}-build"

build() {
     cd ${srcdir}

     msg 'Connecting to GIT server...'

     if [ -d ${_gitname} ]; then
          cd ${_gitname} && git pull origin
          cd ..
     else
          git clone ${_gitroot}
     fi

     msg 'GIT checkout done or server timeout.'

     if [ -d ${_buildir} ]; then
          msg 'Cleaning previous build...'
          rm -rf ${_buildir}
     fi

     git clone ${_gitname} ${_buildir}
     cd ${_buildir}
 }

 package() {
     msg 'Creating package build...'
     cd $srcdir
     # dump just license from the readme
     sed -e :a -e '$q;N;25,$D;ba' android-completion-build/README.markdown > android-completion-build/LICENSE
     install -d $pkgdir/usr/share/bash-completion/completions
     install -m 0755 android-completion-build/android $pkgdir/usr/share/bash-completion/completions/android
     install -m 0755 android-completion-build/adb $pkgdir/usr/share/bash-completion/completions/adb
     install -m 0755 android-completion-build/emulator $pkgdir/usr/share/bash-completion/completions/emulator
     install -m 0755 android-completion-build/fastboot $pkgdir/usr/share/bash-completion/completions/fastboot
     install -m 0755 android-completion-build/repo $pkgdir/usr/share/bash-completion/completions/repo
     install -Dm644 android-completion-build/LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE

}

# vim:syntax=sh
