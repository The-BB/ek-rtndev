#
# Copyright (C) 2017 Jian Chang <aa65535@live.com>
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Original Makefile taken from https://github.com/aa65535/openwrt-simple-obfs
# Deprecated. Followed by v2ray-plugin.

include $(TOPDIR)/rules.mk

PKG_NAME:=simple-obfs
PKG_VERSION:=0.0.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=a9c43588e4cb038e6ac02f050e4cab81f8228dff
PKG_SOURCE_URL:=https://github.com/shadowsocks/simple-obfs.git
PKG_MIRROR_HASH:=d7d28b2cc98e82b15e1c1b4f546a7d8124c853ab858cd6248ebbf1b1e765ab88

PKG_LICENSE:=GPLv3
PKG_LICENSE_FILES:=LICENSE

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf
PKG_BUILD_FLAGS:=no-mips16
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/simple-obfs/Default
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Web Servers/Proxies
	TITLE:=Simple-obfs
	URL:=https://github.com/shadowsocks/simple-obfs
	DEPENDS:=+libev
	MAINTAINER:=Entware team, https://entware.net
endef

Package/simple-obfs = $(call Package/simple-obfs/Default)
Package/simple-obfs-server = $(call Package/simple-obfs/Default)

define Package/simple-obfs/description
 Simple-obfs is a simple obfusacting tool, designed as plugin server of
 shadowsocks.
endef

Package/simple-obfs-server/description = $(Package/simple-obfs/description)

CONFIGURE_ARGS += \
	--disable-ssp \
	--disable-documentation \
	--disable-assert

define Package/simple-obfs/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/obfs-local $(1)/opt/bin
endef

define Package/simple-obfs-server/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/obfs-server $(1)/opt/bin
endef

$(eval $(call BuildPackage,simple-obfs))
$(eval $(call BuildPackage,simple-obfs-server))
