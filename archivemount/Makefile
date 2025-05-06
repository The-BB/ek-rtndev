#
# Copyright (C) 2011-2025 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2020

include $(TOPDIR)/rules.mk

PKG_NAME:=archivemount
PKG_VERSION:=0.9.1
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=78c306538065de9b14f48cfc2024f50f843d3b29
PKG_SOURCE_URL:=https://github.com/cybernoid/archivemount
PKG_MIRROR_HASH:=f83fc069d7157d7d7693a15285972912c5d06515fff67d3053a28ead40e78358

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/archivemount
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Filesystem
	DEPENDS:=+libfuse +libarchive
	TITLE:=FUSE file system for reading archives, supported by libarchive
	URL:=https://cybernoia.de/software/archivemount.html
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/archivemount/description
 Archivemount is a piece of glue code between libarchive
 (http://people.freebsd.org/~kientzle/libarchive/) and FUSE
 (http://fuse.sourceforge.net). It can be used to mount a (possibly compressed)
 archive (as in .tar.gz or .tar.bz2) and use it like an ordinary filesystem.
endef

define Package/archivemount/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/archivemount $(1)/opt/bin
endef

$(eval $(call BuildPackage,archivemount))
