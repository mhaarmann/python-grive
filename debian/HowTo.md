# Make a Ubuntu 18.04 Package
#### Download the Source Package from GitHub, extract it and then run this in your Terminal
#### Replace MY_ID and MY_SECRET!
```
GRIVE_ID="MY_ID"
GRIVE_SECRET="MY_SECRET"

pkgname="python3-grive"
_pkgname="grive"
cd *-${_pkgname}-*/
pkgdir="/tmp/build-$$"
mkdir -p "${pkgdir}"/DEBIAN
echo "{\"client_id\": \"$GRIVE_ID\", \"client_secret\": \"$GRIVE_SECRET\"}" > google-client.json
install -dm755 "${pkgdir}"/usr/lib/sysctl.d
install -dm755 "${pkgdir}"/usr/share/applications
install -dm755 "${pkgdir}"/usr/share/glib-2.0/schemas
install -dm755 "${pkgdir}"/usr/share/${_pkgname}/icons/loader
install -m644 google-client.json "${pkgdir}"/usr/share/${_pkgname}
install -m644 60-${_pkgname}-pyinotify.conf "${pkgdir}"/usr/lib/sysctl.d
install -m644 ${_pkgname}.desktop "${pkgdir}"/usr/share/applications
install -m644 icons/*.png "${pkgdir}"/usr/share/${_pkgname}/icons
install -m644 icons/loader/*.png "${pkgdir}"/usr/share/${_pkgname}/icons/loader
install -m644 apps.${_pkgname}.gschema.xml "${pkgdir}"/usr/share/glib-2.0/schemas
install -m755 ${_pkgname} "${pkgdir}"/usr/share/${_pkgname}
install -m644 LICENSE "${pkgdir}"/usr/share/${_pkgname}
install -m644 debian/control "${pkgdir}"/DEBIAN
pkgsize=$(du -s "${pkgdir}"/usr | cut -f1)
pkgver=$(grep ^Version: "${pkgdir}"/DEBIAN/control | cut -d" " -f2)
sed -i "s/^Installed-Size:.*/Installed-Size: ${pkgsize}/" "${pkgdir}"/DEBIAN/control
bash -c "cd \"${pkgdir}\"; find usr/ -type f -exec md5sum '{}' \; > DEBIAN/md5sums"
dpkg-deb --build "${pkgdir}" ../${pkgname}-${pkgver}_all.deb
```

