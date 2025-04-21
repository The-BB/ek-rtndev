# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2013 Francisco Borges
# Copyright (C) 2011-2025 Entware
#
# Makefile taken from http://github.com/FranciscoBorges/openwrt-printing-packages

include $(TOPDIR)/rules.mk

PKG_NAME:=qpdf
PKG_VERSION:=12.1.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/qpdf/qpdf/tar.gz/refs/tags/v$(PKG_VERSION)?
PKG_HASH:=f1c2d3a26e67ce1b84b2a5165aeb2a1de79e51eeb782b46fcddff87069d7ea1e

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=Apache-2.0 Artistic-2.0-Perl
PKG_LICENSE_FILES:=Artistic-2.0 LICENSE.txt

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/qpdf
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Printing
  TITLE:=PDF transformations utility
  URL:=https://qpdf.sourceforge.io/
  DEPENDS:=+libgnutls +libjpeg +libstdcpp +zlib
endef

define Package/qpdf/description
 QPDF is a command-line program for transformations on PDF files.
endef

CMAKE_BINARY_SUBDIR:=openwrt-build

TARGET_LDFLAGS += -latomic

CMAKE_OPTIONS += \
	-DUSE_IMPLICIT_CRYPTO=0 \
	-DREQUIRE_CRYPTO_GNUTLS=1 \
	-DRANDOM_DEVICE=/dev/urandom

define Package/qpdf/install
	$(INSTALL_DIR) $(1)/opt
	$(CP) $(PKG_INSTALL_DIR)/opt/bin $(1)/opt
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libqpdf.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,qpdf))
