# keepass2_keechallenge

This Dockerfile contains KeePass2 (http://keepass.info) and KeeChallenge (http://sourceforge.net/projects/keechallenge/).

KeeChallenge, in brief, allows you to use a slot on a Yubikey (nearly any, from old 'Standard' on) to store a HMAC-160
challenge-response secret key, and use that as a second factor for KeePass2.  

It precalculates the next HMAC response, and uses that to encrypt the secret for the next round.  That gets stored in an .xml file next to the .kdbx file.  This is naturally vulnerable to replays, but it's not entirely horrible either.

Running a Mono app like KeePass can be dependency-hell-squared.  If you don't need a functional Mono system otherwise, this seems to be a great
candidate for Desktop/GUI Dockerization.

## Use


_my kdbx is in Dropbox_

```
mkdir -p $HOME/.dockerconfigs/keepass2
docker run --rm --device=/dev/bus/usb --device=/dev/usb -v /tmp/.X11-unix:/tmp/.X11-unix -v $HOME/Dropbox:/root/Dropbox -v $HOME/.dockerconfigs/keepass2:/root/.config -e DISPLAY keepass2_keechallenge
```
