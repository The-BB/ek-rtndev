# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# XXX boost bumped

include $(TOPDIR)/rules.mk

PKG_NAME:=cryfs
PKG_VERSION:=0.11.4
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/cryfs/cryfs.git
PKG_MIRROR_HASH:=540d1703945b207d1c5f032cfb95fa48b568cde9c243dc154e66b1a478ea4b6e

PKG_BUILD_DEPENDS:=range-v3 spdlog

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/cryfs
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Filesystem
	DEPENDS:=+boost-chrono +boost-filesystem +boost-program_options \
		 +boost-thread +fuse-utils +libatomic +libcurl +libfmt
	TITLE:=Cryptographic filesystem for the cloud
	URL:=https://www.cryfs.org
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/cryfs/description
 CryFS encrypts your files, so you can safely store them anywhere.
 It works well together with cloud services like Dropbox, iCloud, OneDrive and
 others.
endef

CMAKE_OPTIONS += \
	-DDISABLE_OPENMP=ON \
	-DDISABLE_ASM=ON

define Package/cryfs/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/cryfs{,-unmount} $(1)/opt/bin
endef

$(eval $(call BuildPackage,cryfs))
