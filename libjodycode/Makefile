# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2023-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=libjodycode
PKG_VERSION:=3.1.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://codeberg.org/jbruchon/libjodycode
PKG_MIRROR_HASH:=daa2ecb82269244b2932c12987b2aaa0517bf54ac2951d5ea4a55161f55fe9b1

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE.txt

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libjodycode
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=Jody Bruchon library
	URL:=https://www.jodybruchon.com/software/
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
