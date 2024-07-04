#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cryfs
PKG_VERSION:=0.11.4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/cryfs/cryfs.git
PKG_SOURCE_VERSION:=2c86a6ed376244cb2e3e1fe7e174554b813fcec1
PKG_MIRROR_HASH:=540d1703945b207d1c5f032cfb95fa48b568cde9c243dc154e66b1a478ea4b6e

PKG_BUILD_DEPENDS:=range-v3 spdlog

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/cryfs
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Filesystem
	DEPENDS:=+fuse-utils +libatomic +libcurl +libfmt \
		+boost-program_options +boost-thread +boost-filesystem
	TITLE:=Cryptographic filesystem for the cloud
	URL:=https://www.cryfs.org
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/cryfs/description
 CryFS encrypts your files, so you can safely store them anywhere. It works well
 together with cloud services like Dropbox, iCloud, OneDrive and others.
endef

CMAKE_OPTIONS += \
	-DDISABLE_OPENMP=ON \
	-DDISABLE_ASM=ON

define Package/cryfs/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/cryfs{,-unmount} $(1)/opt/bin
endef

$(eval $(call BuildPackage,cryfs))
