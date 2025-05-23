# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=highlight
PKG_VERSION:=4.15
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://andre-simon.de/zip
PKG_HASH:=68b3f8178c5c9d4b0a03f6948635cef1c8d06244f6b438eebf3a190c588337e9

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING

# remove it if you are using the cmake or meson build system
PKG_INSTALL:=1

PKG_BUILD_DEPENDS:=boost

include $(INCLUDE_DIR)/package.mk
#include $(INCLUDE_DIR)/cmake.mk
#include $(INCLUDE_DIR)/meson.mk

define Package/highlight
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=an universal sourcecode to formatted text converter
  URL:=http://andre-simon.de/
  DEPENDS:=+libstdcpp +lua
endef

define Package/highlight/description
  Highlight converts source code to formatted text with syntax highlighting.
endef

define Package/highlight/conffiles
/opt/etc/highlight/filetypes.conf
endef

# remove it if you are using the cmake or meson build system
Build/Configure:=:

define Package/highlight/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/highlight $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/highlight
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/etc/highlight/filetypes.conf \
		 $(1)/opt/etc/highlight
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/highlight $(1)/opt/share
endef

$(eval $(call BuildPackage,highlight))
