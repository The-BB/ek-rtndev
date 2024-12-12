# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# The newer version (0.25) requires a C++20 compliant compiler.

include $(TOPDIR)/rules.mk

PKG_NAME:=mpdscribble
PKG_VERSION:=0.25
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/MusicPlayerDaemon/mpdscribble
PKG_MIRROR_HASH:=693be4791e94ff38452a493dc4921252e957a5e1e8e8e6d0b6618911a0207056

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

define Package/mpdscribble
	SECTION:=sound
	CATEGORY:=Sound
	TITLE:=MPD client which submits
	URL:=http://www.musicpd.org/clients/mpdscribble/
	DEPENDS:=+libcurl +libgcrypt +libmpdclient +libstdcpp
endef

define Package/mpdscribble/description
 mpdscribble - A Music Player Daemon (MPD) client which submits
 information about tracks being played to a scrobbler (e.g. last.fm).
endef

define Package/mpdscribble/conffiles
/opt/etc/mpdscribble.conf
endef

MESON_ARGS += \
	-Dsystemd=disabled

define Package/mpdscribble/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/mpdscribble $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/mpdscribble.conf $(1)/opt/etc
endef

$(eval $(call BuildPackage,mpdscribble))
