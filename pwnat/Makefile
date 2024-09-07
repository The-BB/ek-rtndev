# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=pwnat
PKG_VERSION:=0.3.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2023-03-31
PKG_SOURCE_VERSION:=c2d3bf4b41fed65ea930ecb345eabe8453310eea
PKG_SOURCE_URL:=https://github.com/samyk/pwnat
PKG_MIRROR_HASH:=2d57cc63d85c7d9789a79dc14955f6b09b265b4c2562d0c500492cb1cd93352d

PKG_VERSION:=$(PKG_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

include $(INCLUDE_DIR)/package.mk

define Package/pwnat
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Firewall
	TITLE:=NAT traversal tool
	URL:=https://samy.pl/pwnat/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/pwnat/description
 The only tool to punch holes through firewalls/NATs where both
 clients and server can be behind separate NATs without any 3rd party
 involvement.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	mkdir $(PKG_BUILD_DIR)/obj
endef

define Package/pwnat/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pwnat $(1)/opt/sbin
endef

$(eval $(call BuildPackage,pwnat))
