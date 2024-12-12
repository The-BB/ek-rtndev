# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=mediainfo
PKG_VERSION:=24.12
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/MediaArea/MediaInfo
PKG_MIRROR_HASH:=cce4d49d1b24f6ebda8b3d86ddf2794312f028019f85476987b3eb2a589af7ec

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
