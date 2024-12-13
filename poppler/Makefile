# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2013 Francisco Borges
# Copyright (C) 2011-2024 Entware

# Makefile taken from http://github.com/FranciscoBorges/openwrt-printing-packages
# 21.12.0+ requires GCC 9.4.0

include $(TOPDIR)/rules.mk

PKG_NAME:=poppler
PKG_VERSION:=24.12.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://poppler.freedesktop.org
PKG_HASH:=1cf374c3146f3f685d9257701bf0c2866c61d6c202c14d1f5c01a1f3a089028a

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING COPYING3

PKG_BUILD_DEPENDS:=boost

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/poppler/Default
	TITLE:=PDF rendering
	URL:=https://poppler.freedesktop.org/
endef

define Package/libpoppler
	$(call Package/poppler/Default)
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE+= library
	DEPENDS:=+fontconfig +lcms +libpng +libstdcpp +libtiff $(ICONV_DEPENDS)
endef

define Package/poppler-utils
	$(call Package/poppler/Default)
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE+= command line utils
	DEPENDS:=+libpoppler
endef

define Package/libpoppler/description
 Poppler is a PDF rendering library based on the xpdf-3.0.
endef

define Package/poppler-utils/description
 Poppler is a PDF rendering command line utils.
endef

TARGET_CXXFLAGS += -pthread
TARGET_LDFLAGS += -lpthread

CMAKE_OPTIONS += \
	-DBUILD_CPP_TESTS=OFF \
	-DBUILD_GTK_TESTS=OFF \
	-DBUILD_MANUAL_TESTS=OFF \
	-DBUILD_QT5_TESTS=OFF \
	-DBUILD_QT6_TESTS=OFF \
	-DENABLE_GPGME=OFF \
	-DENABLE_GOBJECT_INTROSPECTION=OFF \
	-DENABLE_LIBCURL=OFF \
	-DENABLE_LIBOPENJPEG=unmaintained \
	-DENABLE_NSS3=OFF \
	-DENABLE_QT5=OFF \
	-DENABLE_QT6=OFF \
	-DENABLE_UNSTABLE_API_ABI_HEADERS=ON \
	-DENABLE_XPDF_HEADERS=ON

define Package/libpoppler/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libpoppler*.so* $(1)/opt/lib
endef

define Package/poppler-utils/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/pdf* $(1)/opt/bin
endef

$(eval $(call BuildPackage,libpoppler))
$(eval $(call BuildPackage,poppler-utils))
