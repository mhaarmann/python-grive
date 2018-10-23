# Grive (Python)
Google Drive client with support for new Drive REST API (v3) and partial sync
![Alt text](/screenshot.png?raw=true "Screenshot")

Grive can be considered still beta or pre-beta quality. It simply downloads all the files in your Google Drive into a directory. It detect automatic all changes on local and remote Store (Google Drive). After detectings changes, it load your changes back to your local or remote Store. New files created locally or in Google Drive will be uploaded or downloaded respectively. Deleted files will also be "removed" (move to trash). Currently Grive will NOT destroy any of your files: it will only move the files to a directory named ".trash" or put them in the Google Drive trash. You can always recover them!

#### Main features
- Partial Sync a Folder with Google Drive
- Export supported Google Files as "read only" (will be moved to trash and downloaded again, if you make some changes)
- Try to prevent re-downloading and re-uploading if you rename or move something

#### There are a few things that Grive does not do at the moment:
- support for filenames that are double in same folder (should be avoided!).
- support for symbolic links.

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
