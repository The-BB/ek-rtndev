# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=mkvtoolnix
PKG_VERSION:=77.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://mkvtoolnix.download/sources
PKG_HASH:=5f0cb2b7afe39226d0d41bd7ba098db669981da8c4b455862faffae04ca8e57a

PKG_FIXUP:=autoreconf
PKG_BUILD_DEPENDS:=ruby/host pugixml libmatroska

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/mkvtoolnix
	SECTION:=multimedia
	CATEGORY:=Multimedia
	DEPENDS:=+boost-filesystem +boost-system +libflac +libfmt +libgmp +libogg \
		 +libvorbis +qt5-core +zlib $(ICONV_DEPENDS) $(INTL_DEPENDS)
	TITLE:=tools for Matroska files
	URL:=http://matroska.org/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/mkvtoolnix/description
 A set of tools to create, alter and inspect Matroska files.
endef

CONFIGURE_ARGS += \
	--disable-static \
	--disable-gui \
	--disable-qt6 \
	--enable-qt5 \
	--with-boost=$(STAGING_DIR)/opt \
	--with-qmake=$(TOOLCHAIN_DIR)/bin/qmake \
	--without-qt-pkg-config \
	--without-qmake6

CONFIGURE_VARS += \
	QT_CFLAGS="-DQT_CORE_LIB -I$(STAGING_DIR)/opt/include/Qt5/QtCore -I$(STAGING_DIR)/opt/include/Qt5" \
	am_cv_qt5_compilation=1

TARGET_CFLAGS += -Wno-logical-op

TARGET_LDFLAGS += \
	-lstdc++ \
	-lintl \
	-lQt5Core

define Build/Compile
	cd $(PKG_BUILD_DIR); rake
endef

define Package/mkvtoolnix/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/mkv{extract,info,merge,propedit} \
		$(1)/opt/bin
endef

$(eval $(call BuildPackage,mkvtoolnix))
