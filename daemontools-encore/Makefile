# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware
#
# Abandoned in 2018

include $(TOPDIR)/rules.mk

PKG_NAME:=daemontools-encore
PKG_VERSION:=1.11
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=b40600d9ee0aa6025f33f2644207e069315ca64c
PKG_SOURCE_URL:=https://github.com/bruceg/daemontools-encore
PKG_MIRROR_HASH:=fe58cf45587a8e3c4f72eb2f91f60c364128be1cb74d14b23a2b7ff2ddc978cf

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/daemontools-encore
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=a collection of tools for managing UNIX services
	URL:=http://untroubled.org/daemontools-encore/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/daemontools-encore/description
 A collection of tools for managing UNIX services.
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
		echo "$(TARGET_CC) $(TARGET_CFLAGS)" > conf-cc; \
		echo "$(TARGET_CC) $(TARGET_LDFLAGS)" > conf-ld; \
		./makemake \
	)
endef

define Build/Install
	mkdir -p $(PKG_INSTALL_DIR)/opt/bin
	(cd $(PKG_BUILD_DIR); \
		cat BIN | cut -d ':' -f 6 | \
		xargs -d '\n' cp -t $(PKG_INSTALL_DIR)/opt/bin \
	)
endef

define Package/daemontools-encore/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) files/S03daemontools-encore $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/var/service
endef

$(eval $(call BuildPackage,daemontools-encore))
