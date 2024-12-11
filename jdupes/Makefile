# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2017-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=jdupes
PKG_VERSION:=1.28.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://codeberg.org/jbruchon/jdupes
PKG_MIRROR_HASH:=d15e6090bc7ed9d38c1699a41370715a385f3eb6f66af3cf49f96b03afa000ba

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE.txt

PKG_BUILD_DEPENDS:=libjodycode

include $(INCLUDE_DIR)/package.mk

define Package/jdupes
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=duplicate files finder
	URL:=https://www.jdupes.com/
endef

define Package/jdupes/description
 Jdupes is a program for identifying or deleting duplicate files
 residing within specified directories.
endef

MAKE_VARS += \
	ENABLE_BTRFS=1 \
	STATIC_BTRFS_H=1

define Package/jdupes/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/jdupes $(1)/opt/bin
endef

$(eval $(call BuildPackage,jdupes))
