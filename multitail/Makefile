# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=multitail
PKG_VERSION:=7.1.3
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=f24eb8d7706a87504acbeb860906528a4f58dd31
PKG_SOURCE_URL:=https://github.com/folkertvanheusden/multitail.git
PKG_MIRROR_HASH:=aa1c2584e2c8a3a5c27127d3db5e21ce7e8f204b277b01ff1a112cc7645e88a5

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/multitail
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+libncursesw
	TITLE:=log file monitor
	URL:=https://www.vanheusden.com/multitail
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/multitail/description
 MultiTail allows you to monitor logfiles and command output in multiple
 windows in a terminal, colorize, filter and merge.
endef

define Package/multitail/conffiles
/opt/etc/multitail.conf
endef

define Package/multitail/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/multitail $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/multitail.conf.new $(1)/opt/etc/multitail.conf
endef

$(eval $(call BuildPackage,multitail))
