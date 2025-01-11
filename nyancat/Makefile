#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nyancat
PKG_VERSION:=1.5.2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=19f7dcac57bee416f714035947b41df3a76c73a4
PKG_SOURCE_URL:=https://github.com/klange/nyancat
PKG_MIRROR_HASH:=8d53fdef3fff91b413a133fe17b036124b0878ae8d73f76b834e5c3b793a88bd

include $(INCLUDE_DIR)/package.mk

define Package/nyancat
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Nyancat rendered in your terminal
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/nyancat/description
 Nyancat rendered in your terminal.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/src \
		LDFLAGS="$(TARGET_CFLAGS) $(TARGET_LDFLAGS)" \
		CC="$(TARGET_CC)"
endef

define Package/nyancat/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/nyancat $(1)/opt/bin
endef

$(eval $(call BuildPackage,nyancat))
