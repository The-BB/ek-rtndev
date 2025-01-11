# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2022-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=7-zip
PKG_VERSION:=24.09
PKG_RELEASE:=1

PKG_SOURCE:=7z$(subst .,,$(PKG_VERSION))-src.tar.xz
PKG_SOURCE_URL:=https://www.7-zip.org/a
PKG_HASH:=49c05169f49572c1128453579af1632a952409ced028259381dac30726b6133a

PKG_LICENSE:=LGPL-2.0-only

include $(INCLUDE_DIR)/package.mk

PKG_UNPACK:=$(HOST_TAR) -C $(PKG_BUILD_DIR) -xf $(DL_DIR)/$(PKG_SOURCE)

define Package/7-zip
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Compression
	DEPENDS:=+libstdcpp
	TITLE:=file archiver with a high compression ratio
	URL:=https://www.7-zip.org
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/7-zip/description
 File archiver with a high compression ratio.
endef

MAKE_PATH:=CPP/7zip/Bundles/Alone2

MAKE_VARS += \
	MY_ARCH="$(TARGET_CFLAGS) $(TARGET_LDFLAGS)"

define Build/Prepare
	$(PKG_UNPACK)
	chmod +w -R $(PKG_BUILD_DIR)/*
	$(Build/Patch)
endef

define Build/Compile
	$(call Build/Compile/Default,-f makefile.gcc)
endef

define Package/7-zip/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(MAKE_PATH)/_o/7zz $(1)/opt/bin
endef

$(eval $(call BuildPackage,7-zip))
