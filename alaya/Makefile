# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=alaya
PKG_VERSION:=4.6
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/ColumPaget/Alaya
PKG_MIRROR_HASH:=97a4f2446a4346c338b3298db5bb989ac1ef2db1f820dfc4636419f737503930

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENCE

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/alaya
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Web Servers/Proxies
	TITLE:=A WEBDAV Server
	URL:=https://github.com/ColumPaget/Alaya
	DEPENDS:=+libopenssl +libpam +zlib
endef

define Package/alaya/description
 A webdav enabled webserver mostly focused on file storage.
endef

CONFIGURE_ARGS += \
	--enable-xattr \
	--enable-capabilities=no \
	--enable-ssl \
	--enable-ip6 \
	--enable-pam

CONFIGURE_VARS += \
	ac_cv_sys_file_offset_bits=64

define Package/alaya/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/alaya $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/alaya.conf $(1)/opt/etc
	$(INSTALL_BIN) files/S80alaya $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,alaya))
