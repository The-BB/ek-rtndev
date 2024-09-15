#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=automatic
PKG_VERSION:=0.9.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=6301c30c8501c5ec0eb47ec053a4bc82f2e00193
PKG_SOURCE_URL:=https://github.com/1100101/Automatic.git
PKG_MIRROR_HASH:=4301065c951e707336b2f98fa96e57e848b0b3eeffac4d9ad33d53b2cb647d5e

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/automatic
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=BitTorrent
	DEPENDS:=+libcurl +libpcre +libxml2
	TITLE:=RSS torrents downloader
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/automatic/description
 Automatic is a RSS daemon that downloads torrent files matching regular
 expression patterns at certain intervals.
endef

GIT_HEAD:=$(call version_abbrev,$(PKG_SOURCE_VERSION))

define Build/Prepare
	$(call Build/Prepare/Default)
	$(SED) 's|`git rev-parse --short HEAD`|$(GIT_HEAD)|g' \
	    $(PKG_BUILD_DIR)/src/Makefile.am
endef

define Package/automatic/conffiles
/opt/etc/automatic.conf
endef

define Package/automatic/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/automatic $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/automatic.conf-sample $(1)/opt/etc/automatic.conf
	$(INSTALL_BIN) ./files/S91automatic $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,automatic))
