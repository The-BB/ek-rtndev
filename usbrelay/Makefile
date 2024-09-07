# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=usbrelay
PKG_VERSION:=1.2.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=d4225458db37eac4232bd86231a976e91d1cd369
PKG_SOURCE_URL:=https://github.com/darrylb123/usbrelay.git
PKG_MIRROR_HASH:=a51caf6b386bf7cfa4187214f279524793dab4f472bfecb0f34b6c0d5ecf6b87

PKG_BUILD_DEPENDS:=USE_MUSL:argp-standalone

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/usbrelay
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+hidapi
	TITLE:=control usb relay
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/usbrelay/description
 USB Relay driver for linux.
endef

TARGET_LDFLAGS += $(if $(CONFIG_USE_GLIBC),,-largp)

define Package/usbrelay/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/libusbrelay.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,usbrelay))
