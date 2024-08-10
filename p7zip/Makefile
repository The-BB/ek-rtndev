# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=p7zip
PKG_VERSION:=16.02
PKG_RELEASE:=4

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION)_src_all.tar.bz2
PKG_SOURCE_URL:=@SF/p7zip/p7zip/$(PKG_VERSION)
PKG_HASH:=5eb20ac0e2944f6cb9c2d51dd6c4518941c185347d4089ea89087ffdd6e2341f

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)_$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/p7zip
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Compression
	DEPENDS:=+libstdcpp
	TITLE:=Command line version of 7-zip for POSIX systems
	URL:=http://p7zip.sourceforge.net
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/p7zip/description
 Command line version of 7-zip for POSIX systems.
endef

TARGET_CFLAGS += -pthread
TARGET_CXXFLAGS += -pthread

TARGET_CXXFLAGS += -std=c++14

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CXX="$(TARGET_CXX)" \
		ALLFLAGS_C="$(TARGET_CFLAGS)" \
		ALLFLAGS_CPP="$(TARGET_CXXFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		DEST_HOME="$(PKG_INSTALL_DIR)/opt" \
		all4 install
endef

define Package/p7zip/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/7z{,a,r} $(1)/opt/bin
	###
	$(SED) 's,$(PKG_INSTALL_DIR),,' $(1)/opt/bin/*
	$(INSTALL_DIR) $(1)/opt/lib/p7zip/Codecs
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/p7zip/7z{,a,Con*,r} $(1)/opt/lib/p7zip
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/{Client7z,LzmaCon} $(1)/opt/lib/p7zip
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/p7zip/7z.so $(1)/opt/lib/p7zip
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/p7zip/Codecs/*.so $(1)/opt/lib/p7zip/Codecs
endef

$(eval $(call BuildPackage,p7zip))
