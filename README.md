# Grive (Python)
Google Drive client based on Drive REST API (v3) for bidirectional synchronization

![Screenshot](/screenshot.png?raw=true "Screenshot")

Grive automatically downloads all the files from your Google Drive into a local directory and uploads new local files the other way round. It detects all changes on both sides as well. Files deleted in Google Drive get moved to a local trash directory so you can always recover them!

This application can be used to sync files between Google and a computer or just to backup a Google Drive to a local client automatically.

Grive is still in Beta.

#### Main features
- Bidirectional Sync for Google Drive objects
- Removed files on the remote side get moved to a directory named ".trash" on the local side
- Trying to prevent re-downloading and re-uploading after renaming or moving an object
- Download export supported Google Files as "read only" (after changes at Google, local files will be moved to trash and re-downloaded)

#### Not supported yet:
- Identical filenames within the same folder (should be avoided!)
- Symbolic links

___
### Install Grive (for Ubuntu 18.04)
- Install a release [deb-File](https://github.com/john4smith/python-grive/releases) or build a deb-File with the [HowTo](/debian/HowTo.md)

___
### Install Grive (for Arch Linux)
#### Replace GRIVE_ID and GRIVE_SECRET!
#### If you do not have one, you may be able to use it from [Grive2](https://github.com/vitalif/grive2):
- [Client ID](https://github.com/vitalif/grive2/blob/cf51167b55246b7f90ad4970d9686637e8bb0beb/grive/src/main.cc#L49)
- [Client Secret](https://github.com/vitalif/grive2/blob/cf51167b55246b7f90ad4970d9686637e8bb0beb/grive/src/main.cc#L50)

#### Use the [PKGBUILD](https://wiki.archlinux.org/index.php/Makepkg) to make a Package:
```
mkdir -p /tmp/build-$$/; cd /tmp/build-$$/
echo '{"client_id": "GRIVE_ID", "client_secret": "GRIVE_SECRET"}' > /tmp/build-$$/google-client.json
curl -o PKGBUILD https://raw.githubusercontent.com/john4smith/python-grive/master/PKGBUILD
makepkg -d && sudo pacman -U python-grive-*.pkg.tar.xz
```
