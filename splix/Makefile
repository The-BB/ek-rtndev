# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

# XXX switch to git

include $(TOPDIR)/rules.mk

PKG_NAME:=splix
PKG_VERSION:=2.0.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/OpenPrinting/splix
PKG_MIRROR_HASH:=80020aebeaad7339be7f19c8a7972f3c6e4c422356aaa3974011ce860a5c9f59

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/splix
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Printing
  TITLE:=a driver for SPL printers
  URL:=https://openprinting.github.io/splix/
  DEPENDS:= \
	+libcups +libjbig +libjpeg-turbo +libpng +libstdcpp +zlib $(ICONV_DEPENDS)
endef

define Package/splix/description
 Splix is a driver for SPL printers (Samsung and several Xerox printers).
endef

MAKE_VARS += \
	THREADS=1

define Build/Prepare
	$(call Build/Prepare/Default)
	$(CP) $(PKG_BUILD_DIR)/*.ppd $(PKG_BUILD_DIR)/ppd
endef

define Package/splix/install
	$(INSTALL_DIR) $(1)/opt/lib/cups/filter
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/lib/cups/filter/{raster,ps}toqpdl \
			$(1)/opt/lib/cups/filter
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/cups $(1)/opt/share
endef

$(eval $(call BuildPackage,splix))
