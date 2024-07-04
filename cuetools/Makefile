#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cuetools
PKG_VERSION:=1.4.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=365e379483ea180bcfa272d89a2524da55b1d600
PKG_SOURCE_URL:=https://github.com/svend/cuetools.git
PKG_MIRROR_HASH:=2d346cd995b8d3a58d6e05d8cfa3839f79df1ce7a035fbe662f35af7064075e1

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/cuetools
	SECTION:=sound
	CATEGORY:=Sound
	TITLE:=cue and toc file parsers and utilities
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/cuetools/description
 cuetools is a set of utilities for working with Cue Sheet (cue) and
 Table of Contents (toc) files.
endef

define Package/cuetools/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
endef

$(eval $(call BuildPackage,cuetools))
