# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=libmediainfo
PKG_VERSION:=24.12
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/MediaArea/MediaInfoLib
PKG_MIRROR_HASH:=e54fd4644766a6aa8e3345cd2892611a6258d654f75f928b751c94f456aaeb4f

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENSE LICENSE.html

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/libmediainfo
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=library reading metadata from media files
	URL:=https://mediaarea.net/MediaInfo
	DEPENDS:=+libzen +zlib
endef

define Package/libmediainfo/description
 MediaInfo(Lib) is a convenient unified display of the most relevant
 technical and tag data for video and audio files.
endef

CONFIGURE_PATH:=Project/GNU/Library

#CONFIGURE_ARGS += \
#	--with-libcurl=$(STAGING_DIR)/opt

MAKE_PATH:=$(CONFIGURE_PATH)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/include/MediaInfo{,DLL} $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libmediainfo.so* $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libmediainfo.pc $(1)/opt/lib/pkgconfig
endef

define Package/libmediainfo/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libmediainfo.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,libmediainfo))
