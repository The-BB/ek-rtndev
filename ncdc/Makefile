# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=ncdc
PKG_VERSION:=1.25
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://dev.yorhel.nl/download
PKG_HASH:=b9be58e7dbe677f2ac1c472f6e76fad618a65e2f8bf1c7b9d3d97bc169feb740

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/ncdc
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=P2P
	TITLE:=NCurses Direct Connect client
	URL:=https://dev.yorhel.nl/ncdc
	DEPENDS:=+bzip2 +glib2 +libgnutls +libncursesw +libsqlite3 $(ICONV_DEPENDS)
endef

define Package/ncdc/description
 ncdc is a modern and lightweight direct connect client with a friendly
 ncurses interface.
endef

define Build/Compile
	$(HOSTCC) $(PKG_BUILD_DIR)/deps/makeheaders.c -o $(PKG_BUILD_DIR)/makeheaders
	$(call Build/Compile/Default)
endef

define Package/ncdc/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/ncdc $(1)/opt/bin
endef

$(eval $(call BuildPackage,ncdc))
