#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cgdb
PKG_VERSION:=0.8.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=725f91747e4e996e7bbb190410b0e9c4fc594cc9
PKG_SOURCE_URL:=https://github.com/cgdb/cgdb.git
PKG_MIRROR_HASH:=d65edc6fce97a1faf59827ff22ba9a231f44ed5753f957ca4e58c5c21740bdcd

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/cgdb
	SECTION:=devel
	CATEGORY:=Development
	DEPENDS:=+gdb +libstdcpp
	TITLE:=GDB frontend
	URL:=https://cgdb.github.io/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/cgdb/description
 Console front-end to the GNU debugger.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(SED) "s|^AC_INIT(cgdb.*|AC_INIT(cgdb, $(PKG_VERSION))|g" $(PKG_BUILD_DIR)/configure.ac
endef

CONFIGURE_VARS += \
	ac_cv_file__dev_ptmx=yes \
	ac_cv_file__proc_self_status=yes \
	ac_cv_rl_version=8

define Package/cgdb/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cgdb/cgdb $(1)/opt/bin
endef

$(eval $(call BuildPackage,cgdb))
