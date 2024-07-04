#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# XXX BROKEN: new unrar API

include $(TOPDIR)/rules.mk

PKG_NAME:=rar2fs
PKG_VERSION:=1.29.6
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=5ae31771c3f335bbd53882ff70650aba1ab58917
PKG_SOURCE_URL:=https://github.com/hasse69/rar2fs.git
PKG_MIRROR_HASH:=4806b9bcff2a241622bb51e4474482401c99f41cd4aafaf5e02155c5b40b78b7

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/rar2fs
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Filesystem
	DEPENDS:=+libfuse +libunrar +librt $(ICONV_DEPENDS) @BROKEN
	TITLE:=FUSE file system for reading RAR archives
	URL:=https://github.com/hasse69/rar2fs
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/rar2fs/description
 FUSE file system for reading RAR archives.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	mkdir $(PKG_BUILD_DIR)/config
	$(LN) $(PKG_BUILD_DIR)/config.rpath $(PKG_BUILD_DIR)/config/config.rpath
endef

CONFIGURE_ARGS += \
	--with-unrar=$(STAGING_DIR)/opt/include/unrar \
	--with-libiconv-prefix=$(ICONV_PREFIX) \
	--enable-static-unrar=no

define Package/rar2fs/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/{mkr2i,rar2fs} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(LN) /opt/bin/rar2fs $(1)/opt/sbin/mount.rar2fs
endef

$(eval $(call BuildPackage,rar2fs))
