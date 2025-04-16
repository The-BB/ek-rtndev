# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2013 Francisco Borges
# Copyright (C) 2011-2025 Entware

# Makefile taken from http://github.com/FranciscoBorges/openwrt-printing-packages

include $(TOPDIR)/rules.mk

PKG_NAME:=cups-filters
PKG_VERSION:=2.0.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/OpenPrinting/cups-filters/tar.gz/refs/tags/$(PKG_VERSION)?
PKG_HASH:=b0ed43f79b31f0ab27d7d70dffaa62a3b1633f10a9028006671e5019faf63d30

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=COPYING LICENSE

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/cups-filters
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Printing
  TITLE:=OpenPrinting CUPS filters
  URL:=https://openprinting.github.io/
  DEPENDS:= \
	+libcups +libcupsfilters +libjpeg-turbo +libpng +libppd +zlib \
	$(ICONV_DEPENDS)
endef

define Package/cups-filters/description
 CUPS is a standards-based, open-source printing system used by
 Apple's Mac OS® and other UNIX®-like operating systems, especially also Linux.
endef

CONFIGURE_ARGS += \
	--disable-mutool \
	--with-cups-config=$(STAGING_DIR)/opt/bin/cups-config \
	--with-gs-path=/opt/bin/gs \
	--with-ippfind-path=/opt/bin/ippfind \
	--with-shell=/bin/sh

define Package/cups-filters/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/cups $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/{cups,ppd,ppdc} $(1)/opt/share
endef

$(eval $(call BuildPackage,cups-filters))
