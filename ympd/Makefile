# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# Abandoned in 2018

include $(TOPDIR)/rules.mk

PKG_NAME:=ympd
PKG_REAL_VERSION:=1.3.0
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2018-03-29
PKG_SOURCE_VERSION:=612f8fc0b2c47fc89d403e4a044541c6b2b238c8
PKG_SOURCE_URL:=https://github.com/notandy/ympd
PKG_MIRROR_HASH:=502d721d564969eef7b422198cc83c0236531e2f04613b15507b4178ae97a5fa

PKG_VERSION:=$(PKG_REAL_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/ympd
	SECTION:=sound
	CATEGORY:=Sound
	TITLE:=MPD Web GUI
	URL:=http://www.ympd.org/
	DEPENDS:=+libmariadb +libopenssl
endef

define Package/ympd/description
 Standalone MPD Web GUI written in C, utilizing Websockets and Bootstrap/JS.
endef

define Package/ympd/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/ympd $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S90ympd $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,ympd))
