# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=radare2
PKG_VERSION:=5.9.8
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/radareorg/radare2
PKG_MIRROR_HASH:=7484ac97a82afbd97a833196f197fbf84dc04ae2388887db744eaa59c2e37eac

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-only LGPL-3.0-only
PKG_LICENSE_FILES:=COPYING COPYING.LESSER

PKG_BUILD_DEPENDS:=python3/host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

define Package/radare2
	SECTION:=devel
	CATEGORY:=Development
	TITLE:=reverse engineering framework
	URL:=https://www.radare.org/
	DEPENDS:=+(mips||mipsel):libatomic +libuv
endef

define Package/radare2/description
 UNIX-like reverse engineering framework and command-line toolset.
endef

ifeq ($(or $(CONFIG_mips),$(CONFIG_mipsel)),y)
TARGET_LDFLAGS+=-latomic
endif

define Package/radare2/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/bin $(1)/opt
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libr_*.so* $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/share/radare2
	$(CP) $(PKG_INSTALL_DIR)/opt/share/radare2/$(PKG_VERSION) \
		$(1)/opt/share/radare2
	$(SED) '1c\#!/opt/bin/r2 -j' \
		$(1)/opt/share/radare2/$(PKG_VERSION)/scripts/licenses.r2.js
endef

$(eval $(call BuildPackage,radare2))
