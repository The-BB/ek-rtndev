#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=jo
PKG_VERSION:=1.9
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=2cc476178198774ad6bea89be0b9e4ed2d4bf4c5
PKG_SOURCE_URL:=https://github.com/jpmens/jo
PKG_MIRROR_HASH:=c22d1dcccaba1d9f8f01f866009a150846a7d398b2c0926f465cad2caff6504a

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/jo
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=JSON output from a shell
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/jo/description
 jo is a small utility to create JSON objects.
endef

define Package/jo/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/jo $(1)/opt/bin
endef

$(eval $(call BuildPackage,jo))
