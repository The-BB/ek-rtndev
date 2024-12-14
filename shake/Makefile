# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=shake
PKG_REAL_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2022-03-13
PKG_SOURCE_VERSION:=8d7fe0596a2dc9b38aabd7640ffc29254ddd92fd
PKG_SOURCE_URL:=https://github.com/unbrice/shake
PKG_MIRROR_HASH:=538a9344bbc8e4494573896bfcbed235a3834a994b54d8967a2c353cc088aadc

PKG_VERSION:=$(PKG_REAL_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=COPYING GPL.txt

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/shake
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Filesystem
	TITLE:=defragmentation utility
	URL:=https://vleu.net/projects/shake/
	DEPENDS:=+libattr
endef

define Package/shake/description
 Shake is a defragmenter that runs in userspace.
endef

TARGET_CFLAGS += \
	-I$(STAGING_DIR)/opt/include

define Package/shake/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/{shake,unattr} $(1)/opt/bin
endef

$(eval $(call BuildPackage,shake))
