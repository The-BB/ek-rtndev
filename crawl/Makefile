# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=crawl
PKG_VERSION:=0.32.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/crawl/crawl/tar.gz/$(PKG_VERSION)?
PKG_HASH:=8b9330a9a8156a7b93cc0964b5cc7cba8312f0cf745b64a072432f17f67f889d

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=python-yaml/host

include $(INCLUDE_DIR)/package.mk

define Package/crawl
	SECTION:=games
	CATEGORY:=Games
	TITLE:=Dungeon Crawl Stone Soup is a role-playing roguelike game
	URL:=https://crawl.develz.org
	DEPENDS:=+liblua +libncursesw +libsqlite3 +libstdcpp +zlib
endef

define Package/crawl/description
 Dungeon Crawl Stone Soup is an open-source, single-player, role-playing
 roguelike game of exploration and treasure-hunting in dungeons filled
 with dangerous and unfriendly monsters in a quest to rescue
 the mystifyingly fabulous Orb of Zot.
endef

MAKE_PATH:=crawl-ref/source

define Build/Configure
	echo $(PKG_VERSION) > $(PKG_BUILD_DIR)/crawl-ref/source/util/release_ver
endef

MAKE_FLAGS += \
	prefix=/opt \
	DESTDIR=$(PKG_INSTALL_DIR) \
	DATADIR=/opt/share/crawl/ \
	SAVEDIR=/opt/var/crawl/ \
	NO_TRY_GOLD=yes \
	install

define Package/crawl/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/crawl $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/share/crawl
	$(CP) $(PKG_INSTALL_DIR)/opt/share/crawl/* $(1)/opt/share/crawl
	$(INSTALL_DIR) $(1)/opt/var/crawl/{morgue,saves}
endef

define Package/crawl/postrm
#!/bin/sh

rm -rf /opt/share/crawl
echo Crawl saves \(~5Mb\) still is in /opt/var/crawl
echo You may delete it manually later.
endef

$(eval $(call BuildPackage,crawl))
