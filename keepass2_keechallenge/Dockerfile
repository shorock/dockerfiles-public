# VERSION:		0.2
# DESCRIPTION:	Create keepass2 container with KeeChallenge
# AUTHOR:       Tom Shorock <thomas@shorock.com
# HATTIP:		Jérémy DECOOL <contact@jdecool.fr>
# HATTIP:       Ben Rush <http://sourceforge.net/u/brush701/profile/> for KeeChallenge
# USAGE:
#
#  Container with KeePass2 and the KeeChallenge (http://sourceforge.net/projects/keechallenge/) HMAC OTP
#    second-factor for YubiKeys
#
#	# Build keepass2_keechallenge image
#	docker build -t keepass2 .
#
#
#   # Keeping state is handy
#   mkdir -p $HOME/.dockerconfigs/keepass2
#
#	# Run the container and mount your keepass2 database file
#	docker run --rm \
#		-v /tmp/.X11-unix:/tmp/.X11-unix \
#       -v $HOME/Dropbox:/root/Dropbox \
#       -v $HOME/.dockerconfigs/keepass2:/root/.config \
#       --device=/dev/bus/usb --device=/dev/usb
#		-e DISPLAY \
#		keepass2
#
# ISSUES:
#	# 'Gtk: cannot open display: :0'
#	Try to set 'DISPLAY=your_host_ip:0' or run 'xhost +' on your host.
#	(see: http://stackoverflow.com/questions/28392949/running-chromium-inside-docker-gtk-cannot-open-display-0)
#
# # TODO:
#   It'd be nice to be smarter about which USB devices this container actually needs
#   That's more of a matter for the wrapping shell script/alias than for the Dockerfile


FROM ubuntu:wily
MAINTAINER Tom Shorock <thomas@shorock.com>

RUN apt-get update && apt-get install -y \
	keepass2 libykpers-1-1 libjson0 libusb-1.0-0 libyubikey0 libmono-system-core4.0-cil wget unzip

ENV KEECHALLENGE_URL="http://downloads.sourceforge.net/project/keechallenge/KeeChallenge/bin/KeeChallenge_1.4_win.zip" \
    KEECHALLENGE_SHA256SUM="092be01ed4c025ab7fd9c5046b36625398c22ff6a5858aa775938a47cf030bd7  KeeChallenge_1.4_win.zip"

RUN wget http://downloads.sourceforge.net/project/keechallenge/KeeChallenge/bin/KeeChallenge_1.4_win.zip  && \
    echo $KEECHALLENGE_SHA256SUM | sha256sum -c - && \
    unzip -d /usr/lib/keepass2 KeeChallenge_1.4_win.zip && \
    rm KeeChallenge_1.4_win.zip






CMD ["/usr/bin/keepass2"]
