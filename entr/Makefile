# PDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=entr
PKG_VERSION:=5.6
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=3cd81272a2838fe5628de7f18ca45418792cca20
PKG_SOURCE_URL:=https://github.com/eradman/entr.git
PKG_MIRROR_HASH:=a6763c80ee79995de0762d2dd3b48a57e6e9b53c6d5e4b12affb6910f6639c59

include $(INCLUDE_DIR)/package.mk

define Package/entr
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=run arbitrary commands when files change
	URL:=http://eradman.com/entrproject/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/entr/description
 A utility for running arbitrary commands when files change.
endef

define Build/Configure
	$(LN) $(PKG_BUILD_DIR)/Makefile.linux-compat $(PKG_BUILD_DIR)/Makefile
endef

define Package/entr/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/entr $(1)/opt/bin
endef

$(eval $(call BuildPackage,entr))
