# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# This is the last version without G_SockList objects

include $(TOPDIR)/rules.mk

PKG_NAME:=ngrok-c
PKG_REAL_VERSION:=1.45
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2018-05-07
PKG_SOURCE_VERSION:=990efc7efa325689697c2bc3807f5753a39d74b7
PKG_SOURCE_URL:=https://github.com/dosgo/ngrok-c
PKG_MIRROR_HASH:=dd36a10140968df16ac6b1c64d35e8f7bdc7569af47f7c46a2292b8f3f9adb89

PKG_VERSION:=$(PKG_REAL_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/ngrok-c
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Web Servers/Proxies
	TITLE:=client of ngrok in language C
	URL:=$(PKG_SOURCE_URL)
	DEPENDS:=+libopenssl +libstdcpp
endef

define Package/ngrok-c/description
 ngrok client written in C.
endef

define Package/ngrok-c/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ngrokc $(1)/opt/sbin
endef

$(eval $(call BuildPackage,ngrok-c))
