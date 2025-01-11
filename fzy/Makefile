#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fzy
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=f5d41e726cd997ba038815e218c48017228a8f0e
PKG_SOURCE_URL:=https://github.com/jhawthorn/fzy
PKG_MIRROR_HASH:=8cccf212be5683318eda499d1c5b4ee6c5f04238dc144acc45d5b3b6c2fd1d23

include $(INCLUDE_DIR)/package.mk

define Package/fzy
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Filesystem
	TITLE:=fuzzy finder for the terminal
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/fzy/description
 fzy is a fast, simple fuzzy text selector for the terminal
 with an advanced scoring algorithm.
endef

define Package/fzy/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fzy $(1)/opt/bin
endef

$(eval $(call BuildPackage,fzy))
