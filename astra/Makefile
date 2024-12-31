#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2017

include $(TOPDIR)/rules.mk

PKG_NAME:=astra
PKG_VERSION:=4.4.188
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=646cc63bdf14d3da29b00a8da5c697fa9dcb31e2
PKG_SOURCE_URL:=https://bitbucket.org/cesbo/astra
PKG_MIRROR_HASH:=a6127f39bc0b7d345196e24e27eb2274217795a4b83c70225c6e19f33344c80c

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

define Package/astra
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=advanced streamer
	DEPENDS:=+libopenssl
	URL:=https://cesbo.com/en/astra/
endef

define Package/astra/description
 Astra is a software to organize Digital TV Broadcasting Service.
endef

define Build/Configure
	cd $(PKG_BUILD_DIR); \
	./configure.sh \
		--cc="$(TARGET_CC)" \
		--cflags="$(TARGET_CFLAGS) $(EXTRA_CFLAGS) $(TARGET_CPPFLAGS) $(EXTRA_CPPFLAGS)" \
		--ldflags="$(TARGET_LDFLAGS) -lssl -lcrypto"
endef

define Package/astra/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/astra $(1)/opt/bin/astra
endef

$(eval $(call BuildPackage,astra))
