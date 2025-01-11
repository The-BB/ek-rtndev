#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mqtt-exec
PKG_VERSION:=0.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=da665e304315bc0f60069bf5bf7d610b7eaebb02
PKG_SOURCE_URL:=https://github.com/ncopa/mqtt-exec
PKG_MIRROR_HASH:=37f67b93f4b6fc5691faa1c41fa08e357b3c1f701d75c4c069e1900a84255504

include $(INCLUDE_DIR)/package.mk

define Package/mqtt-exec
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libmosquitto-ssl
	TITLE:=mqtt subscriber that executes a command
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/mqtt-exec/description
 A simple mqtt subscriber that executes a command on mqtt messages
endef

define Package/mqtt-exec/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mqtt-exec $(1)/opt/bin
endef

$(eval $(call BuildPackage,mqtt-exec))
