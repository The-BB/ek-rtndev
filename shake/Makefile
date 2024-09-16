# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2021 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=shake
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2017-07-02
PKG_SOURCE_VERSION:=33dd09dfd77dba8e73da194d2ea4c1e0d9c90ace
PKG_SOURCE_URL:=https://github.com/unbrice/shake.git
PKG_MIRROR_HASH:=8a9137c02ea87c3a96691a2ebae11835b4945338b45a4546b7664e4f4f2f16e3

PKG_VERSION:=$(PKG_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/shake
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Filesystem
	DEPENDS:=+libattr @!USE_MUSL
	TITLE:=defragmentation utility
	URL:=http://vleu.net/shake/
	MAINTAINER:=Entware team, https://entware.net
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
