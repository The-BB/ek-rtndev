# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# The newer version requires g++10
# XXX boost bumped

include $(TOPDIR)/rules.mk

PKG_NAME:=mpdscribble
PKG_VERSION:=0.24
PKG_RELEASE:=5

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=a0ae861f2349c676eebedfbcebfae0b61090b6fb
PKG_SOURCE_URL:=https://github.com/MusicPlayerDaemon/mpdscribble.git
PKG_MIRROR_HASH:=af0b80e355ba139da3a8965d707970cddf5507e3aa7326479250ccd0958e0c4e

PKG_BUILD_DEPENDS:=boost

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

define Package/mpdscribble
	SECTION:=sound
	CATEGORY:=Sound
	DEPENDS:=+libgcrypt +libmpdclient +libcurl +libstdcpp
	TITLE:=MPD player with Last.fm scrobbler
	URL:=http://mpd.wikia.com/wiki/Client:Mpdscribble
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/mpdscribble/description
 MPD scribble is a music player daemon client which submits information about
 tracks being played to Last.fm.
endef

MESON_ARGS += \
	-Dsystemd=disabled

MESON_VARS += BOOST_ROOT=$(STAGING_DIR)/opt

TARGET_CFLAGS += $(shell $(STAGING_DIR)/opt/bin/libgcrypt-config --cflags)
TARGET_LDFLAGS += $(shell $(STAGING_DIR)/opt/bin/libgcrypt-config --libs)

define Package/mpdscribble/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/mpdscribble $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/mpdscribble.conf $(1)/opt/etc
endef

define Package/mpdscribble/conffiles
/opt/etc/mpdscribble.conf
endef

$(eval $(call BuildPackage,mpdscribble))
