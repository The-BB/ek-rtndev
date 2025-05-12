# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2017-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=man-db
PKG_VERSION:=2.13.0
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://gitlab.com/man-db/man-db/-/archive/$(PKG_VERSION)
PKG_HASH:=adb430f71afd46ab5a5743d25cf966a3af9742bf40af072f90918a991dfae8b8

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/man-db
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Tools for reading manual pages
  URL:=https://man-db.gitlab.io/man-db/
  DEPENDS:= +groff +less +libgdbm +libpipeline +libunistring +zlib \
	$(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

define Package/man-db/description
 This package provides the man command, the primary way of examining
 the help files (manual pages).
endef

define Package/man-db/conffiles
/opt/etc/man_db.conf
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

CONFIGURE_ARGS += \
	--mandir=/opt/share/man \
	--disable-setuid \
	--with-device=latin1 \
	--with-pager=less \
	--disable-cache-owner \
	--disable-manual \
	--disable-nls \
	--disable-year2038 \
	--with-libiconv-prefix="$(ICONV_PREFIX)" \
	--with-libintl-prefix="$(INTL_PREFIX)"

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

define Package/man-db/install
	$(INSTALL_DIR) $(1)/opt/{bin,etc,lib/man-db,sbin,share,var/cache/man}
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/{catman,lexgrog,man{,db,path,-recode},whatis} \
			$(1)/opt/bin
	$(LN) whatis $(1)/opt/bin/apropos
	$(INSTALL_CONF) ./files/man_db.conf $(1)/opt/etc
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/man-db/{globbing,manconv,zsoelim} \
			$(1)/opt/lib/man-db
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/man-db/libman{,db}*.so $(1)/opt/lib/man-db
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/accessdb $(1)/opt/sbin
	$(CP) $(PKG_INSTALL_DIR)/opt/share $(1)/opt
endef

$(eval $(call Download,gnulib))
$(eval $(call BuildPackage,man-db))
