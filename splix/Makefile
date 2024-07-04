#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2013

include $(TOPDIR)/rules.mk

PKG_NAME:=splix
PKG_VERSION:=2.0.0
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=svn
PKG_SOURCE_VERSION:=315
PKG_SOURCE_URL:=https://svn.code.sf.net/p/splix/code/splix
PKG_MIRROR_HASH:=aaf4c18e4f44d641c4a13c8944e8339299848c47303234cb01f49e0585aa118a

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/splix
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Printing
	DEPENDS:=+cups +libjbig
	TITLE:=Samsung CUPS drivers
	URL:=http://splix.ap2c.org/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/splix/description
 SpliX is a set of CUPS printer drivers for SPL (Samsung Printer Language)
 printers.
endef

MAKE_VARS += \
	THREADS=1

define Build/Configure
	$(CP) $(PKG_BUILD_DIR)/*.ppd $(PKG_BUILD_DIR)/ppd
endef

define Package/splix/install
	$(INSTALL_DIR) $(1)/opt/lib/cups/filter
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/cups/filter/{raster,ps}toqpdl \
	    $(1)/opt/lib/cups/filter
	$(INSTALL_DIR) $(1)/opt/share/cups/model
	$(CP) $(PKG_INSTALL_DIR)/opt/share/cups/model/* $(1)/opt/share/cups/model
endef

$(eval $(call BuildPackage,splix))
