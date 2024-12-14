# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2021 Entware

# Abandoned in 2013

include $(TOPDIR)/rules.mk

PKG_NAME:=splix
PKG_REAL_VERSION:=2.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=svn
PKG_SOURCE_VERSION:=315
PKG_SOURCE_URL:=https://svn.code.sf.net/p/splix/code/splix
PKG_MIRROR_HASH:=70cb02ff69b58ca948ccda8d8721f3ed5e9b4b3ec756b52e2bd064961489b736

PKG_VERSION:=$(PKG_REAL_VERSION)_svn~$(PKG_SOURCE_VERSION)

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/splix
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Printing
	TITLE:=Samsung CUPS drivers
	URL:=http://splix.ap2c.org/
	DEPENDS:=+cups +libjbig
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
