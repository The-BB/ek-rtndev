# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=pingu
PKG_VERSION:=1.5.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/ncopa/pingu
PKG_MIRROR_HASH:=564770cfc630584ce81900a7ce942331bb3dda3150a9d12347413c6adb2ddba3

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=
PKG_LICENSE_FILES:=

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/pingu
	SECTION:=net
	CATEGORY:=Network
	TITLE:=policy routing daemon with failover
	URL:=$(PKG_SOURCE_URL)
	DEPENDS:=+libev
endef

define Package/pingu/description
 Pingu is a daemon that takes care of policy routing and fail-over
 in multi ISP setups. Support for DHCP, PPP, ISP failover, Load-balancing
 (nexthop), optional route rule based on fwmark, run script when ISP goes
 up/down.
endef

CONFIGURE_ARGS:= \
	--prefix=/opt \
	--disable-doc

TARGET_CFLAGS += $(FPIC)

define Package/pingu/conffiles
/opt/etc/pingu.conf
endef

define Package/pingu/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/mtu $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/pingu{,ctl} $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/pingu.conf $(1)/opt/etc
	$(INSTALL_BIN) files/S11pingu $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,pingu))
