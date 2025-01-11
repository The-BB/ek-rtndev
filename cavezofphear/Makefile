#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cavezofphear
PKG_VERSION:=0.6.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=fa0b1b1cb87b7de8beee6b1e658da90e6bd52d31
PKG_SOURCE_URL:=https://github.com/AMDmi3/cavezofphear
PKG_MIRROR_HASH:=651a3d129ea73fc3661002ccb1d1d5fd4d7fbd9fd44d2c2948fb80437cb8ac7a

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS += \
	-DWITH_MANPAGE=OFF \
	-DSYSTEMWIDE=ON

define Package/cavezofphear
	SECTION:=games
	CATEGORY:=Games
	DEPENDS:=+libncurses
	TITLE:=CAVEZ of PHEAR is a boulder dash / digger like game
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/cavezofphear/description
 CAVEZ of PHEAR is a boulder dash / digger like game for console / terminals
 using ncurses. The goal of this game is to escape through the caves by
 collecting diamonds and avoid falling stones.
endef

define Package/cavezofphear/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/phear $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/phear $(1)/opt/share
endef

$(eval $(call BuildPackage,cavezofphear))
