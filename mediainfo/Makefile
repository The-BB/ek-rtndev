# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=mediainfo
PKG_VERSION:=25.03
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/MediaArea/MediaInfo
PKG_MIRROR_HASH:=6554decbd45f11dc5125626aa036db860a436d33de91365e679fbae19f225b6f

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENSE LICENSE.html

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/mediainfo
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=command-line utility
	URL:=https://mediaarea.net/MediaInfo
	DEPENDS:=+libmediainfo
endef

define Package/mediainfo/description
 MediaInfo is a convenient unified display of the most relevant
 technical and tag data for video and audio files.
endef

CONFIGURE_PATH:=Project/GNU/CLI
MAKE_PATH:=$(CONFIGURE_PATH)

define Package/mediainfo/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_BUILD_DIR)/$(CONFIGURE_PATH)/mediainfo $(1)/opt/bin
endef

$(eval $(call BuildPackage,mediainfo))
