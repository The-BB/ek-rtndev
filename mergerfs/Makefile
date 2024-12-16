# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2020-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=mergerfs
PKG_VERSION:=2.40.2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/trapexit/mergerfs
PKG_MIRROR_HASH:=1a1240e05ae2a4ecf3aea6b7012c39c0b259ae300fed8444fa93a0f3c547a7e2

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=ISC
PKG_LICENSE_FILES:=LICENSE

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/mergerfs
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Filesystem
	TITLE:=a featureful union filesystem
	URL:=$(PKG_SOURCE_URL)
	DEPENDS:=+(mips||mipsel):libatomic +libstdcpp
endef

define Package/mergerfs/description
 mergerfs is a union filesystem geared towards simplifying storage and
 management of files across numerous commodity storage devices. It is similar
 to mhddfs, unionfs, and aufs.
endef

PKG_FILE_MODES:=/opt/bin/mergerfs-fusermount:root:root:4755

ifeq ($(or $(CONFIG_mips),$(CONFIG_mipsel)),y)
TARGET_LDFLAGS+=-latomic
endif

Build/Configure:=:

define Package/mergerfs/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/mergerfs{,-fusermount} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/mount.mergerfs $(1)/opt/sbin
endef

$(eval $(call BuildPackage,mergerfs))
