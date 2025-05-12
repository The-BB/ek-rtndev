# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2018-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=libpipeline
PKG_VERSION:=1.5.8
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://gitlab.com/libpipeline/libpipeline/-/archive/$(PKG_VERSION)
PKG_HASH:=ada309694ee87ed564a798e7f6ceab70f577f922e0c0e2fe81018ddfe218ca51

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libpipeline
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=pipeline manipulation library
  URL:=https://libpipeline.gitlab.io/libpipeline/
endef

define Package/libpipeline/description
 libpipeline is a C library for setting up and running pipelines of processes.
endef

GNULIB_SRC_DATE:=2024-06-30
GNULIB_SRC_FILE:=gnulib-$(GNULIB_SRC_DATE).tar.zst
define Download/gnulib
  PROTO:=git
  FILE:=$(GNULIB_SRC_FILE)
  SOURCE_VERSION:=0ba13435a9362bec0ff5fd0830907b9fac723e41
  URL:=https://git.savannah.gnu.org/git/gnulib.git
  SUBDIR:=gnulib
  MIRROR_HASH:=9f3443d7c0aedf6ca602a37d11177c633d9bd3f87373827137c5737daa33765c
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(TAR) -xf $(DL_DIR)/$(GNULIB_SRC_FILE) -C $(PKG_BUILD_DIR)
endef

define Build/Configure
	( cd $(PKG_BUILD_DIR); \
		GNULIB_TOOL_IMPL=sh \
		./bootstrap \
		--gnulib-srcdir=gnulib \
		--no-git; \
	)
	$(call Build/Configure/Default)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/pipeline.h $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libpipeline.so* $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libpipeline.pc $(1)/opt/lib/pkgconfig
endef

define Package/libpipeline/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libpipeline.so* $(1)/opt/lib
endef

$(eval $(call Download,gnulib))
$(eval $(call BuildPackage,libpipeline))
