# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=bip
PKG_VERSION:=0.9.3
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=0a93c8cfd336c209c5e3d41e9188bab5bba55d0b
PKG_SOURCE_URL:=https://vcs-git.duckcorp.org/projects/bip/bip.git
PKG_MIRROR_HASH:=5e39184eb5f3b3c11f89a524ad5c86d6816e6d76f5c50c1343209693b3e959b3

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/bip
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Instant Messaging
	TITLE:=multi user IRC proxy
	URL:=https://projects.duckcorp.org/projects/bip
	DEPENDS:=+libopenssl
endef

define Package/bip/description
 Bip is an IRC proxy, which means it keeps connected to your preferred
 IRC servers, can store the logs for you, and even send them back to your
 IRC client(s) upon connection.
endef

define Package/bip/conffiles
/opt/etc/bip.conf
endef

define Package/bip/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/bip{,mkpw} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) \
		$(PKG_INSTALL_DIR)/opt/share/doc/bip/examples/bip.conf \
			$(1)/opt/etc
	$(INSTALL_BIN) ./files/S99bip $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,bip))
