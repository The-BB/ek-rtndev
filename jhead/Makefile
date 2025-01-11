#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=jhead
PKG_VERSION:=3.08
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=4d04ac965632e35a65709c7f92a857a749e71811
PKG_SOURCE_URL:=https://github.com/Matthias-Wandel/jhead
PKG_MIRROR_HASH:=43e9a789449fc63b90e4107b484b766c6b45a3dc082d093317ce345285933b23

include $(INCLUDE_DIR)/package.mk

define Package/jhead
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=Exif Jpeg header manipulation tool
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/jhead/description
 Exif Jpeg header manipulation tool.
endef

define Package/jhead/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/jhead $(1)/opt/bin
endef

$(eval $(call BuildPackage,jhead))
