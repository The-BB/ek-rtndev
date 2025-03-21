# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2023-2025 Entware
#
# only build static library (neovim)

include $(TOPDIR)/rules.mk

PKG_NAME:=tree-sitter
PKG_VERSION:=0.24.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/tree-sitter/tree-sitter/tar.gz/refs/tags/v$(PKG_VERSION)?
PKG_HASH:=03c7ee1e6f9f4f3821fd4af0ae06e1da60433b304a73ff92ee9694933009121a

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libtree-sitter
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=an incremental parsing library
  URL:=https://tree-sitter.github.io
  BUILDONLY:=1
endef

define Package/libtree-sitter/description
 Tree-sitter is a parser generator tool and an incremental parsing
 library. It can build a concrete syntax tree for a source file and efficiently
 update the syntax tree as the source file is edited.
endef

Build/Configure:=:

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/* $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libtree-sitter.a $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/*.pc $(1)/opt/lib/pkgconfig
endef

$(eval $(call BuildPackage,libtree-sitter))
