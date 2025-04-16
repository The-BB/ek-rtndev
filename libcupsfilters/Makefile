# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=libcupsfilters
PKG_VERSION:=2.1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/OpenPrinting/libcupsfilters/tar.gz/refs/tags/$(PKG_VERSION)?
PKG_HASH:=26dc9dc502d811c6f7e24ddea54dac5e7b8db2e2781e6ec6854ec98cc3260f45

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=COPYING LICENSE

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/libcupsfilters
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Printing
  TITLE:=OpenPrinting libcupsfilters
  URL:=https://openprinting.github.io/
  DEPENDS:= \
	+fontconfig +lcms +libcups +libdbus +libexif +libfreetype +libjpeg-turbo \
	+libpng +libpoppler +libstdcpp +libtiff +qpdf +zlib $(ICONV_DEPENDS)
  DEPENDS+=+dejavu-fonts-ttf-DejaVuSans +dejavu-fonts-ttf-DejaVuSansMono
endef

define Package/libcupsfilters/description
  Library providing everything for filtering/converting print/scan job data.
endef

CONFIGURE_ARGS += \
	--disable-mutool \
	--with-cups-config=$(STAGING_DIR)/opt/bin/cups-config \
	--with-gs-path=/opt/bin/gs \
	--with-ippfind-path=/opt/bin/ippfind \
	--with-test-font-path=/opt/share/fonts/dejavu/DejaVuSans.ttf

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/cupsfilters $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcupsfilters.{a,so*} $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/*.pc $(1)/opt/lib/pkgconfig
endef

define Package/libcupsfilters/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcupsfilters.so* $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/cups $(1)/opt/share
endef

$(eval $(call BuildPackage,libcupsfilters))
