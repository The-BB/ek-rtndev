# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2021 Entware

# Project archieved

include $(TOPDIR)/rules.mk

PKG_NAME:=nfusr
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2019-03-19
PKG_SOURCE_VERSION:=4c21b69f201b50b8f1dd3aac0125baa3b5d02ade
PKG_SOURCE_URL:=https://github.com/facebookarchive/nfusr.git
PKG_MIRROR_HASH:=a56106eac203b648a5f96f18a6e5bb7ef704d20f595e3b77b279fb7fb8016b48

PKG_VERSION:=$(PKG_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/nfusr
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Filesystem
	DEPENDS:=+libstdcpp +fuse-utils +libnfs $(ICONV_DEPENDS) $(INTL_DEPENDS)
	TITLE:=a userspace FUSE client for accessing NFSv3 servers
	URL:=https://github.com/facebookincubator/nfusr
	MAINTAINER:=Entware team, https://entware.net
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
