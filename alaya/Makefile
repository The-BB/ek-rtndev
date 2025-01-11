# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=alaya
PKG_VERSION:=4.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=00c9d13732ee48d2020bebe14329532c06d2a02d
PKG_SOURCE_URL:=https://github.com/ColumPaget/Alaya
PKG_MIRROR_HASH:=2431463d47c524c1defd42bf6888b1e1c331ad4b9c4167ffad9882f4fea8e5ab

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/alaya
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Web Servers/Proxies
	TITLE:=A WEBDAV Server
	URL:=https://sites.google.com/site/columscode/home/Alaya
	DEPENDS:=+libopenssl +libcap +libpam
	MAINTAINER:=Entware team, https://entware.net
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

TARGET_CFLAGS += \
	-I$(STAGING_DIR)/opt/include

TARGET_LDFLAGS += \
	-lssl -lcrypto

define Package/alaya/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/alaya $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/alaya.conf $(1)/opt/etc
	$(INSTALL_BIN) files/S80alaya $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,alaya))
