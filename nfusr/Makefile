# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# Project archieved

include $(TOPDIR)/rules.mk

PKG_NAME:=nfusr
PKG_REAL_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-03-19
PKG_SOURCE_VERSION:=4c21b69f201b50b8f1dd3aac0125baa3b5d02ade
PKG_SOURCE_URL:=https://github.com/facebookarchive/nfusr
PKG_MIRROR_HASH:=a56106eac203b648a5f96f18a6e5bb7ef704d20f595e3b77b279fb7fb8016b48

PKG_VERSION:=$(PKG_REAL_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/nfusr
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Filesystem
	TITLE:=NFS client in userspace
	URL:=https://github.com/facebookincubator/nfusr
	DEPENDS:=+fuse-utils +libnfs +libstdcpp $(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

define Package/nfusr/description
 nfusr is a userspace FUSE client for accessing NFSv3 servers based on libnfs.
endef

TARGET_CPPFLAGS += -D_LARGEFILE64_SOURCE -D_FILE_OFFSET_BITS=64 -D_GNU_SOURCE

define Package/nfusr/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/$(PKG_NAME) $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/sbin/mount.$(PKG_NAME) $(1)/opt/sbin
endef

$(eval $(call BuildPackage,nfusr))
