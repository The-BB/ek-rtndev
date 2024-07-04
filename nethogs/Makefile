#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nethogs
PKG_VERSION:=0.8.7
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=ea161b050991b92f8d17e6fb6fb4cfae8cf1915d
PKG_SOURCE_URL:=https://github.com/raboof/nethogs.git
PKG_MIRROR_HASH:=2bab9e7d0a5b93ad2976ef3400d6027db5bad1a5a1b98c88843bc3b0c7721041

include $(INCLUDE_DIR)/package.mk

define Package/nethogs
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libncurses +libpcap +libstdcpp
	TITLE:=NetHogs is a small 'net top' tool
	URL:=https://github.com/raboof/nethogs
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/nethogs/description
 NetHogs is a small 'net top' tool. Instead of breaking the traffic down per
 protocol or per subnet, like most tools do, it groups bandwidth by process.
 If there's suddenly a lot of network traffic, you can fire up NetHogs and
 immediately see which PID is causing this. This makes it easy  to indentify
 programs that have gone wild and are suddenly taking up your bandwidth.
endef

TARGET_CFLAGS += $(TARGET_CPPFLAGS) $(TARGET_LDFLAGS) -fPIC

define Package/nethogs/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/nethogs $(1)/opt/sbin
endef

$(eval $(call BuildPackage,nethogs))
