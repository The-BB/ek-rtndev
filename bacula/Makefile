# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2006-2015 OpenWrt.org
# Copyright (C) 2015-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=bacula
PKG_VERSION:=15.0.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/bacula
PKG_HASH:=294afd3d2eb9d5b71c3d0e88fdf19eb513bfdb843b28d35c0552e4ae062827a1

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENSE-FOSS

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/bacula
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Open Source Network Backup Solution
	URL:=https://www.bacula.org/
	DEPENDS:=+gawk +libacl +libcap +liblzo +libopenssl +libsqlite3
	DEPENDS+=+libstdcpp +libwrap +libzstd $(INTL_DEPENDS)
endef

define Package/bacula/description
 Bacula is a set of computer programs that permits the system administrator to
 manage backup, recovery, and verification of computer data across a network of
 computers of different kinds. Bacula can also run entirely upon a single
 computer and can backup to various types of media, including tape and disk.
endef

CONFIGURE_VARS += \
	ac_cv_func_setpgrp_void=yes \
	ac_cv_func_chflags=no \
	ac_cv_sys_file_offset_bits=64 \
	ac_cv_sys_large_files=yes \
	ac_cv_sys_largefile_CFLAGS=-D_LARGFILE_SOURCE \
	ac_cv_sys_largefile_LDFLAGS= \
	ac_cv_sys_largefile_LIBS= \
	ac_cv_sys_largefile_source=yes

CONFIGURE_ARGS += \
	--disable-conio \
	--disable-static \
	--enable-largefile \
	--enable-readline \
	--enable-smartalloc \
	--sysconfdir=/opt/etc/bacula/ \
	--with-archivedir=/opt/bacula/tmp \
	--with-openssl=$(STAGING_DIR)/opt \
	--with-pid-dir=/opt/var/run \
	--with-readline=$(STAGING_DIR)/opt \
	--with-scriptdir=/opt/etc/bacula/scripts \
	--with-sqlite3=$(STAGING_DIR)/opt \
	--with-subsys-dir=/opt/var/run/subsys \
	--with-tcp-wrappers=$(STAGING_DIR)/opt \
	--without-x

define Package/bacula/conffiles
/opt/etc/bacula/bacula-dir.conf
/opt/etc/bacula/bacula-fd.conf
/opt/etc/bacula/bacula-sd.conf
/opt/etc/bacula/bconsole.conf
endef

define Package/bacula/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/* $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/*.so* $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/etc/bacula/scripts
	$(INSTALL_DIR) $(1)/opt/bacula/tmp
	$(INSTALL_DIR) $(1)/opt/bacula/working
	$(INSTALL_DIR) $(1)/opt/bacula/log
	$(INSTALL_DIR) $(1)/opt/var/run/subsys/
	$(CP) $(PKG_INSTALL_DIR)/opt/etc/bacula/*.conf $(1)/opt/etc/bacula
	$(CP) $(PKG_INSTALL_DIR)/opt/etc/bacula/scripts/* $(1)/opt/etc/bacula/scripts
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S* $(1)/opt/etc/init.d
	# XXX
	$(SED) 's,$(STAGING_DIR),,g;s,$(TOOLCHAIN_DIR),/opt,g; \
		s,$(STAGING_DIR_HOST),/opt,g; \
		s,/lib/libiconv-full,,g;s,/lib/libintl-full,,g; \
		s,-f\(file\|macro\)-prefix-map=$(PKG_BUILD_DIR)=$(PKG_NAME)-$(PKG_VERSION),,g' \
			$(1)/opt/etc/bacula/scripts/bacula_config
# create_sqlite3_database, grant_sqlite3_privileges, make_sqlite3_tables, update_sqlite3_tables
	$(SED) 's,$(STAGING_DIR),,g' $(1)/opt/etc/bacula/scripts/*
	$(SED) 's,^!#.*python,#!/opt/bin/python,' \
		$(1)/opt/etc/bacula/scripts/key-manager.py \
		$(1)/opt/sbin/md5tobase64.py
	$(SED) 's,^!#.*perl,#!/opt/bin/perl,' $(1)/opt/sbin/get_malware_abuse.ch
endef

$(eval $(call BuildPackage,bacula))
