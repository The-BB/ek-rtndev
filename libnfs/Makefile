# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

# The newer version is incompatible with nfusr

include $(TOPDIR)/rules.mk

PKG_NAME:=libnfs
PKG_VERSION:=5.0.3
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/sahlberg/libnfs
PKG_MIRROR_HASH:=fefc07c59b38bf7283cc23cf4590948ff0e5f966dd636e2cc7f221c1b82dde1a

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=LGPL-2.1-only
PKG_LICENSE_FILES:=COPYING LICENSE-BSD.txt LICENSE-GPL-3.txt LICENSE-LGPL-2.1.txt

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libnfs/Default
	SUBMENU:=Filesystem
	TITLE:=NFS client library
	URL:=$(PKG_SOURCE_URL)
endef

define Package/libnfs
	$(call Package/libnfs/Default)
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE+= (shared library)
endef

define Package/libnfs-utils
	$(call Package/libnfs/Default)
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE+= (binaries)
	DEPENDS:=+libnfs
endef

define Package/libnfs/description
 LIBNFS is a client library for accessing NFS shares over a network.
endef

define Package/libnfs-utils/description
 nfs-cat, nfs-cp, nfs-ls console usersapce utilities for accessing
 NFS shares over a network.
endef

CMAKE_OPTIONS += \
	-DENABLE_UTILS=ON

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/nfsc $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libnfs.so* $(1)/opt/lib
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
