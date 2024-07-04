# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2023-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=libjodycode
PKG_VERSION:=3.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=e44699edc8915f65635d2fa1c9dcfac38b1784c7
PKG_SOURCE_URL:=https://codeberg.org/jbruchon/libjodycode.git
PKG_MIRROR_HASH:=7bce927e85787e63e73e4279cc9936a3b1f0e5f6da2b8ebea3ef4418142a4c3a

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libjodycode
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=Jody Bruchon library
	URL:=https://www.jodybruchon.com/software
	MAINTAINER:=Entware team, https://entware.net
	BUILDONLY:=1
endef

define Package/libjodycode/description
 Shared code used by several utilities written by Jody Bruchon.
endef

MAKE_VARS += PREFIX=/opt

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/include/$(PKG_NAME).h $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/$(PKG_NAME).a $(1)/opt/lib
endef

$(eval $(call BuildPackage,libjodycode))
