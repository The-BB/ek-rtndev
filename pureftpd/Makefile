# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=pureftpd
PKG_VERSION:=1.0.52
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/jedisct1/pure-ftpd
PKG_MIRROR_HASH:=c77b7553c607bf615dbcde16c46bcb829f58da9f2adb068b9d1ab4834701821b

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=ISC
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/pureftpd
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=File Transfer
	TITLE:=Pure FTP server
	URL:=https://www.pureftpd.org/
	DEPENDS:=+libmariadb +libopenssl +libsodium +zlib
endef

define Package/pureftpd/description
 Pure-FTPd is a fast, production-quality, standard-conformant FTP server,
 based upon Troll-FTPd.
endef

CONFIGURE_ARGS += \
	--with-certfile=/opt/etc/ssl/private/pure-ftpd.pem \
	--with-everything \
	--with-mysql \
	--with-paranoidmsg \
	--with-tls \
	--with-virtualchroot \
	--without-capabilities

define Package/pureftpd/conffiles
/opt/etc/pure-ftpd.conf
endef

define Package/pureftpd/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/pure-* $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/pure-* $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/pure-* $(1)/opt/etc
	$(INSTALL_BIN) ./files/S65pureftpd $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,pureftpd))
