# PDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=entr
PKG_VERSION:=5.7
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/eradman/entr
PKG_MIRROR_HASH:=09e09689618b4cbb5f6b37c2cc5359ac4c04f1b6a56081ec19fdb4cf6d72dbad

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=ISC
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/entr
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=run arbitrary commands when files change
	URL:=https://eradman.com/entrproject/
endef

define Package/entr/description
 A utility for running arbitrary commands when files change.
endef

MAKE_FLAGS += -f Makefile.linux-compat

Build/Configure:=:

define Package/entr/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/entr $(1)/opt/bin
endef

$(eval $(call BuildPackage,entr))
