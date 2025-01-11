#
# Copyright (C) 2020-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=aha
PKG_VERSION:=0.5.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=41c2320eb31ef1c95fcd45a0feb0303f606fc711
PKG_SOURCE_URL:=https://github.com/theZiz/aha
PKG_MIRROR_HASH:=26e3a8473dbfdce3fc8b8b6aac4971e0a10df51879df0346d972a782324a49ef

include $(INCLUDE_DIR)/package.mk

define Package/aha
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Ansi HTML Adapter
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/aha/description
 Converts ANSI escape sequences of a unix terminal to HTML code.
endef

define Package/aha/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/aha $(1)/opt/bin
endef

$(eval $(call BuildPackage,aha))
