# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=libmediainfo
PKG_VERSION:=24.06
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=547f070e74f1054ebd8ef17e36f8e9d7b6e53e92
PKG_SOURCE_URL:=https://github.com/MediaArea/MediaInfoLib.git
PKG_MIRROR_HASH:=07ce815e5cae48b18ae73dc3c819516d27075b7600da7325a7dc0fc369c3c817

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
