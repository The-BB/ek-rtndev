#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=wg-quick
PKG_VERSION:=1.0.20210914
PKG_RELEASE:=1

PKG_SOURCE:=wireguard-tools-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://git.zx2c4.com/wireguard-tools/snapshot
PKG_HASH:=97ff31489217bb265b7ae850d3d0f335ab07d2652ba1feec88b734bc96bd05ac

include $(INCLUDE_DIR)/package.mk

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_UNPACK:= $(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xf $(DL_DIR)/$(PKG_SOURCE)

define Package/wg-quick
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=VPN
	URL:=https://www.wireguard.com
	MAINTAINER:=Jason A. Donenfeld <Jason@zx2c4.com>
	TITLE:=WireGuard wg-quick script
	DEPENDS:=+bash +coreutils-stat
	PKGARCH:=all
endef

define Package/wg-quick/description
 This is an extremely simple script for easily bringing up a WireGuard
 interface, suitable for a few common use cases.
endef

define Build/Compile
endef

define Package/wg-quick/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/wg-quick/linux.bash $(1)/opt/bin/wg-quick
endef

$(eval $(call BuildPackage,wg-quick))
