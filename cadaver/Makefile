# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2012 Erinome.net
# Copyright (C) 2013-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=cadaver
PKG_VERSION:=0.26
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://notroj.github.io/cadaver
PKG_HASH:=9236e43cdf3505d9ef06185fda43252840105c0c02d9370b6e1077d866357b55

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/cadaver
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Filesystem
	TITLE:=Command-line WebDAV client
	URL:=https://notroj.github.io/cadaver/
	DEPENDS:= \
		+libexpat +libncurses +libneon +libopenssl +libreadline +zlib \
		$(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

define Package/cadaver/description
 cadaver is a command-line WebDAV client for Unix. It supports file upload,
 download, on-screen display, namespace operations (move/copy), collection
 creation and deletion, and locking operations.
endef

CONFIGURE_ARGS += \
	--with-ssl=openssl \
	--without-gssapi

TARGET_CPPFLAGS += -D_LARGEFILE64_SOURCE -D_FILE_OFFSET_BITS=64 -D_GNU_SOURCE

define Package/cadaver/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/cadaver $(1)/opt/bin
endef

$(eval $(call BuildPackage,cadaver))
