# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=libmediainfo
PKG_VERSION:=24.01
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=51dbd89651ac45b169d2f80ac3e966f5c7451a00
PKG_SOURCE_URL:=https://github.com/MediaArea/MediaInfoLib.git
PKG_MIRROR_HASH:=48290955d1f958f47ac85b684227e08ec3d13b102673c03c84ad51cfd2670a6a

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/libmediainfo
	SECTION:=libs
	CATEGORY:=Libraries
	DEPENDS:=+libzen +zlib
	TITLE:=Mediainfo support library
	URL:=http://mediaarea.net/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/libmediainfo/description
 LibediaInfo is a convenient unified display of the most relevant technical and tag data for
 video and audio files.
endef

CONFIGURE_PATH:=Project/GNU/Library

#CONFIGURE_ARGS += \
#	--with-libcurl=$(STAGING_DIR)/opt

MAKE_PATH:=$(CONFIGURE_PATH)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/include/MediaInfo $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/MediaInfoDLL $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libmediainfo.so* $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libmediainfo.pc $(1)/opt/lib/pkgconfig
endef

define Package/libmediainfo/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libmediainfo.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,libmediainfo))
