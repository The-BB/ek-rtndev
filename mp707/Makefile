#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2016

include $(TOPDIR)/rules.mk

PKG_NAME:=mp707
PKG_VERSION:=1.0.2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=d0874e415be034637041e261cbcf2aed378bf917
PKG_SOURCE_URL:=https://github.com/bubbafix/openwrt-bm1707.git
PKG_MIRROR_HASH:=dc3e3fe16bccac3c93379e2e08a2eb3f9655f7729d3edd47b3aa98f6093e1d06

include $(INCLUDE_DIR)/package.mk

define Package/mp707
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+libusb-compat +libstdcpp
	TITLE:=USB thermometer MP707(BM1707) utility
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/mp707/description
 This utility works with USB thermometer MP707 (BM1707).
 More information on device can be found at http://www.masterkit.ru
endef

define Build/Compile
	$(TARGET_CXX) $(TARGET_CXXFLAGS) -c -I$(STAGING_DIR)/opt/include -o $(PKG_BUILD_DIR)/$(PKG_NAME).o $(PKG_BUILD_DIR)/package/bmtemp/src/bmtemp.cpp
	$(TARGET_CXX) $(TARGET_LDFLAGS) -L$(STAGING_DIR)/opt/lib -o $(PKG_BUILD_DIR)/bmtemp $(PKG_BUILD_DIR)/$(PKG_NAME).o -lusb
endef

define Package/mp707/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bmtemp $(1)/opt/bin
endef

$(eval $(call BuildPackage,mp707))
