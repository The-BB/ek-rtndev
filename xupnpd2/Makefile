# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=xupnpd2
PKG_REAL_VERSION:=2.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2023-12-15
PKG_SOURCE_VERSION:=9dc123d7e034b338ef5824c390d1b4ae8b2cf639
PKG_SOURCE_URL:=https://github.com/clark15b/xupnpd2
PKG_MIRROR_HASH:=bb6524c547ce6751fcb5ce476be396f25e35fd7c18c7c1dd987d0a94c588baca

PKG_VERSION:=$(PKG_REAL_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/xupnpd2
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=eXtensible UPnP agent v.2
	URL:=https://github.com/clark15b/xupnpd2
	DEPENDS:=+liblua5.3 +libopenssl +libsqlite3 +libstdcpp +libuuid
endef

define Package/xupnpd2/description
 Xupnpd2 is a complete cross-platform media server with the
 ability to broadcast IPTV and OTT into local network, as well as video,
 photos and music from the home archive to any a DLNA-compatible device.
endef


define Package/xupnpd2/conffiles
/opt/etc/xupnpd2/xupnpd.cfg
/opt/etc/xupnpd2/xupnpd.lua
endef

define Build/Configure
	echo 'include build/rules.mk' > $(PKG_BUILD_DIR)/Makefile
endef

ifeq ($(CONFIG_USE_MUSL),y)
TARGET_CXXFLAGS += -D_LARGEFILE64_SOURCE
endif

TARGET_CXXFLAGS += -I$(STAGING_DIR)/opt/include/lua5.3

TARGET_LDFLAGS += -ldl -luuid -lsqlite3 -llua5.3 -lssl -lcrypto


define Package/xupnpd2/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/xupnpd $(1)/opt/sbin/xupnpd2
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S94xupnpd2 $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/etc/xupnpd2
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/xupnpd.{cfg,lua} $(1)/opt/etc/xupnpd2
	$(INSTALL_DIR) $(1)/opt/share/xupnpd2/media
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/media/example.m3u \
		$(1)/opt/share/xupnpd2/media
	$(CP) $(PKG_BUILD_DIR)/www $(1)/opt/share/xupnpd2
endef

$(eval $(call BuildPackage,xupnpd2))
