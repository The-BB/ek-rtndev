# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=multitail
PKG_VERSION:=7.1.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/folkertvanheusden/multitail
PKG_MIRROR_HASH:=8e21f68e3913d0e2e606359080d52a5bfe811f3b4582b7d29b406c9ad21a2461

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/multitail
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=log file monitor
	URL:=https://www.vanheusden.com/multitail
	DEPENDS:=+libncursesw
endef

define Package/multitail/description
 MultiTail allows you to monitor logfiles and command output in
 multiple windows in a terminal, colorize, filter and merge.
endef

define Package/multitail/conffiles
/opt/etc/multitail.conf
endef

define Package/multitail/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/multitail $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/multitail.conf.new \
		$(1)/opt/etc/multitail.conf
endef

$(eval $(call BuildPackage,multitail))
