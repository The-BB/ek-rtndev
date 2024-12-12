# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2017-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=msd
PKG_VERSION:=3.2.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=2975b18a02cad4887d2032d0944bc2179fb0a560
PKG_SOURCE_URL:=https://github.com/rozhuk-im/msd
PKG_MIRROR_HASH:=499d488fdaaa2abbd9e78a022a65c98e74c9d24767a6ed8e85685d3c1982be61

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/msd
	SECTION:=multimedia
	CATEGORY:=Multimedia
	SUBMENU:=Streaming
	TITLE:=program for IP TV streaming on the network via HTTP
	URL:=http://www.netlab.linkpc.net/wiki/en:software:msd:index
endef

define Package/msd/description
 Multi stream daemon. Program for organizing IP TV streaming on the
 network via HTTP.
endef

define Package/msd/conffiles
/opt/etc/msd_channels2.conf
/opt/etc/msd_channels.conf
/opt/etc/msd.conf
/opt/etc/msd_minimal.conf
endef

define Package/msd/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/msd $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/msd
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/conf/*.conf $(1)/opt/etc
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S29msd $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,msd))
