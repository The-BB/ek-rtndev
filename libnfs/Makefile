# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2021 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=libnfs
PKG_VERSION:=5.0.3
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=4379837536d9eac537810dc7b13071136049b22a
PKG_SOURCE_URL:=https://github.com/sahlberg/libnfs.git
PKG_MIRROR_HASH:=fefc07c59b38bf7283cc23cf4590948ff0e5f966dd636e2cc7f221c1b82dde1a

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/libnfs/Default
	SUBMENU:=Filesystem
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/libnfs
	$(call Package/libnfs/Default)
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=client library for accessing NFS shares over a network
endef

define Package/libnfs-utils
	$(call Package/libnfs/Default)
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+libnfs
	TITLE:=libnfs utilities
endef

define Package/libnfs/description
 LIBNFS is a client library for accessing NFS shares over a network.
endef

define Package/libnfs-utils/description
 nfs-ls, nfs-cat, nfs-cp console usersapce utilities for accessing NFS shares
 over a network.
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/* $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/* $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libnfs.pc $(1)/opt/lib/pkgconfig
endef

define Package/libnfs/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libnfs.so* $(1)/opt/lib
endef

define Package/libnfs-utils/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
endef

$(eval $(call BuildPackage,libnfs))
$(eval $(call BuildPackage,libnfs-utils))
