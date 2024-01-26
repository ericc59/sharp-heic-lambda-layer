# # Library Versions
# WEBP_VERSION=1.3.2
# LIBDE265_VERSION=1.0.15
# LIBHEIF_VERSION=1.17.6
# VIPS_VERSION=8.15.1
# SHARP_VERSION=0.33.2

# PREFIX_PATH=/opt

# export PKG_CONFIG_PATH=$(PREFIX_PATH)/lib/pkgconfig

# build-SharpHEICLayer: installLib libvips libwebp libde265 libheif
# 	mkdir -p "$(ARTIFACTS_DIR)/nodejs"
# 	mkdir -p "$(ARTIFACTS_DIR)/lib"

# 	# sharp uses several of the libs we installed or compiled. extract the full list and copy all of those into /opt/lib
# 	# extract list with ldd from sharp.node, manipulate a bit with sed to only get the absolute paths, then copy
# 	LD_LIBRARY_PATH=$(PREFIX_PATH)/lib npm --prefix "$(ARTIFACTS_DIR)/nodejs/" install sharp@$(SHARP_VERSION) --include=optional

# 	ls -al $(ARTIFACTS_DIR)/nodejs/node_modules/sharp/
# 	LD_LIBRARY_PATH=$(PREFIX_PATH)/lib ldd $(ARTIFACTS_DIR)/nodejs/node_modules/sharp/build/Release/sharp-linux-x64.node | sed -nE "s/^[^\/\n]*(\/[^ ]+)(.*)/\1/p" | xargs cp -t $(ARTIFACTS_DIR)/lib

# libwebp:
# 	curl -L https://github.com/webmproject/libwebp/archive/v$(WEBP_VERSION).tar.gz | tar zx
# 	cd libwebp-$(WEBP_VERSION) && ./autogen.sh && ./configure --enable-libwebpmux --prefix=$(PREFIX_PATH) && make V=0 && make install

# libde265:
# 	# libde265
# 	curl -L https://github.com/strukturag/libde265/releases/download/v$(LIBDE265_VERSION)/libde265-$(LIBDE265_VERSION).tar.gz | tar zx
# 	cd libde265-$(LIBDE265_VERSION) && ./autogen.sh && ./configure --disable-dec265 --disable-sherlock265 --prefix=$(PREFIX_PATH) && make V=0 && make install

# libheif: libde265
# 	# libheif
# 	curl -L https://github.com/strukturag/libheif/releases/download/v$(LIBHEIF_VERSION)/libheif-$(LIBHEIF_VERSION).tar.gz | tar zx
# # 	# cd libheif-$(LIBHEIF_VERSION) && ./autogen.sh && ./configure --prefix=$(PREFIX_PATH) && make V=0 && make install
# 	cd libheif-$(LIBHEIF_VERSION) && mkdir build && cd build && cmake3 --preset=release .. && make && make install

# libvips: installLib libheif libwebp
# # 	# libvips
# 	# curl -L https://github.com/libvips/libvips/releases/download/v$(VIPS_VERSION)/vips-$(VIPS_VERSION).tar.gz | tar zx
# 	  curl -L https://github.com/libvips/libvips/releases/download/v$(VIPS_VERSION)/vips-$(VIPS_VERSION).tar.xz | tar xJ
# 	# cd vips-$(VIPS_VERSION) && ./configure --prefix=$(PREFIX_PATH) && make V=0 && make install
# 	cd vips-$(VIPS_VERSION) && meson setup build --prefix $(PREFIX_PATH) && cd build && ninja && ninja install

# installLib:
# 	dnf update -y

# 	dnf install -y gcc-c++
# 	dnf install -y meson ninja-build

# 	# Install and enable the EPEL RPM package on Amazon Linux 2
# 	# yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
# 	# dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm

# 	# Install the RPM Fusion configuration package
# 	# yum install -y https://download1.rpmfusion.org/free/el/rpmfusion-free-release-9.noarch.rpm
# 	# dnf install -y https://download1.rpmfusion.org/free/el/rpmfusion-free-release-9.noarch.rpm

# 	# Install the Remi repository configuration package
# 	# yum install -y https://rpms.remirepo.net/enterprise/remi-release-9.rpm
# 	#   dnf install -y https://rpms.remirepo.net/enterprise/remi-release-9.rpm


# 	# Install the yum-utils package (for the yum-config-manager command)
# 	yum install -y yum-utils

# 	# Enable Remi's RPM repository
# 	# yum-config-manager --enable remi

# 	yum install -y \
# 		glib2-devel \
# 		expat-devel \
# 		lcms2-devel \
# 		libjpeg-devel \
# 		libjpeg-turbo-devel \
# 		libpng-devel \
# 		giflib-devel \
# 		libexif-devel \
# 		librsvg2-devel \
# 		libtiff-devel \
# 		poppler-devel \
# 		poppler-glib \
# 		cmake3

# 	# Install libvips with HEIC support (+ development files and command-line tools)
# 	# yum install -y vips vips-heif vips-devel vips-tools --skip-broken

# Library Versions
WEBP_VERSION=1.3.2
LIBDE265_VERSION=1.0.12
LIBHEIF_VERSION=1.12.0
VIPS_VERSION=8.12.2
SHARP_VERSION=0.33.2
POPPLER_VERSION=24.01.0
GPGME_VERSION=1.23.2
QT_VERSION=6.6.1

PREFIX_PATH=/opt

export PKG_CONFIG_PATH=$(PREFIX_PATH)/lib/pkgconfig

build-SharpHEICLayer: libvips
	mkdir -p "$(ARTIFACTS_DIR)/nodejs"
	mkdir -p "$(ARTIFACTS_DIR)/lib"

	# sharp uses several of the libs we installed or compiled. extract the full list and copy all of those into /opt/lib
	# extract list with ldd from sharp.node, manipulate a bit with sed to only get the absolute paths, then copy
	npm install -g node-addon-api node-gyp
	LD_LIBRARY_PATH=$(PREFIX_PATH)/lib npm --prefix "$(ARTIFACTS_DIR)/nodejs/" install --build-from-source sharp@$(SHARP_VERSION)
	LD_LIBRARY_PATH=$(PREFIX_PATH)/lib ldd $(ARTIFACTS_DIR)/nodejs/node_modules/sharp/build/Release/sharp-linux-x64.node | sed -nE "s/^[^\/\n]*(\/[^ ]+)(.*)/\1/p" | xargs cp -t $(ARTIFACTS_DIR)/lib

libwebp:
	curl -L https://github.com/webmproject/libwebp/archive/v$(WEBP_VERSION).tar.gz | tar zx
	cd libwebp-$(WEBP_VERSION) && ./autogen.sh && ./configure --enable-libwebpmux --prefix=$(PREFIX_PATH) && make V=0 && make install

libde265:
	# libde265
	curl -L https://github.com/strukturag/libde265/releases/download/v$(LIBDE265_VERSION)/libde265-$(LIBDE265_VERSION).tar.gz | tar zx
	cd libde265-$(LIBDE265_VERSION) && ./autogen.sh && ./configure --disable-dec265 --disable-sherlock265 --prefix=$(PREFIX_PATH) && make V=0 && make install

libheif: libde265
	# libheif
	curl -L https://github.com/strukturag/libheif/releases/download/v$(LIBHEIF_VERSION)/libheif-$(LIBHEIF_VERSION).tar.gz | tar zx
	cd libheif-$(LIBHEIF_VERSION) && ./autogen.sh && ./configure --prefix=$(PREFIX_PATH) && make V=0 && make install

gpgme:
	# gpgme
	curl -L https://gnupg.org/ftp/gcrypt/gpgme/gpgme-$(GPGME_VERSION).tar.bz2 | tar xj
	cd gpgme-$(GPGME_VERSION) && ./configure --prefix=$(PREFIX_PATH) && make V=0 && make install

qt6:
	# qt6
	curl -L https://download.qt.io/official_releases/qt/6.6/$(QT_VERSION)/single/qt-everywhere-src-$(QT_VERSION).tar.xz | tar xJ
	cd qt-everywhere-src-$(QT_VERSION) && ./configure --prefix=$(PREFIX_PATH) && make V=0 && make install

libpoppler:
	# libpoppler
	curl -L https://poppler.freedesktop.org/poppler-$(POPPLER_VERSION).tar.xz | tar xJ
	git clone git://git.freedesktop.org/git/poppler/test test
	cd poppler-$(POPPLER_VERSION) && mkdir build && cd build && cmake3 .. -DCMAKE_INSTALL_PREFIX=$(PREFIX_PATH) -DCMAKE_BUILD_TYPE=release && make && make install

libvips: installLib gpgme qt6 libpoppler libheif libwebp 
	# libvips
	curl -L https://github.com/libvips/libvips/releases/download/v$(VIPS_VERSION)/vips-$(VIPS_VERSION).tar.gz | tar zx
	cd vips-$(VIPS_VERSION)

	./configure --prefix=$(PREFIX_PATH) && make V=0 && make install




installLib:
	# dnf update -y
	# yum install -y dnf-plugin-ovl && \
	dnf update -y
	yum update -y
	# dnf install -y qt5-qtbase qt5-qtbase-devel 
	yum install -y \
		glib2-devel \
		expat-devel \
		libjpeg-devel \
		libjpeg-turbo-devel \
		libpng-devel \
		giflib-devel \
		libexif-devel \
		librsvg2-devel \
		libtiff-devel \
		lcms2-devel \
		cmake3
	yum install -y nss nss-tools nss-devel cairo libjpeg libpng libtiff
	# yum install -y python3-distutils
	pip install setuptools