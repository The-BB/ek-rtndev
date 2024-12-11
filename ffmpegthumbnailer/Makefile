# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2006-2011 OpenWrt.org
# Copyright (C) 2015-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=ffmpegthumbnailer
PKG_VERSION:=2.2.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/dirkvdb/ffmpegthumbnailer/tar.gz/refs/tags/$(PKG_VERSION)?
PKG_HASH:=8c9b9057c6cc8bce9d11701af224c8139c940f734c439a595525e073b09d19b8

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libffmpegthumbnailer
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=library to create thumbnails
	URL:=https://github.com/dirkvdb/ffmpegthumbnailer
	DEPENDS:=+libffmpeg-full +libjpeg +libpng +libstdcpp
endef

define Package/libffmpegthumbnailer/description
 libffmpegthumbnailer is a library that can be used to create thumbnails
 for your video files.
endef

define Package/libffmpegthumbnailer/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libffmpegthumbnailer*.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libffmpegthumbnailer))
