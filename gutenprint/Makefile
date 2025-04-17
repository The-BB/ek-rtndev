# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

# Based on https://github.com/FranciscoBorges/openwrt-printing-packages

include $(TOPDIR)/rules.mk

PKG_NAME:=gutenprint
PKG_VERSION:=5.3.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@SF/gimp-print
PKG_HASH:=f5a9f47de28530b1ae2069cfbc647a9a641baeeabe809bb0ef2b3ec5b9668d70

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DEPENDS:=gutenprint/host
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

HOST_PATCH_DIR:=

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/gutenprint
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Printing
  TITLE:=Gutenprint Top Quality Printer Drivers
  URL:=https://gimp-print.sourceforge.io/
  DEPENDS:= \
	+libcups +libjpeg-turbo +libncursesw +libpng +libreadline +libusb-1.0 \
	+zlib $(ICONV_DEPENDS)
endef

define Package/gutenprint/description
 High quality drivers for Canon, Epson, Lexmark, Sony, Olympus, and PCL
 printers for use with CUPS and GIMP.
endef

HOST_CONFIGURE_ARGS += \
	--disable-escputil \
	--disable-nls \
	--disable-nls-macosx \
	--disable-samples \
	--disable-shared \
	--disable-test \
	--without-cups \
	--without-doc \
	--without-gimp2 \
	--without-modules \
	--without-readline

define Host/Compile
	$(MAKE) $(HOST_JOBS) -C $(HOST_BUILD_DIR)/src/xml \
		$(HOST_MAKE_FLAGS) extract-strings
endef

define Host/Install
endef

CONFIGURE_ARGS += \
	--disable-test

define Build/Configure
	$(call Build/Configure/Default)
	$(LN) $(HOST_BUILD_DIR)/src/xml/extract-strings \
		$(PKG_BUILD_DIR)/src/xml/extract-strings
endef

define Package/gutenprint/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/cups $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libgutenprint.so* $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/cups-genppd.5.3 $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/share/gutenprint
	$(CP) $(PKG_INSTALL_DIR)/opt/share/cups $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/gutenprint/5.3 $(1)/opt/share/gutenprint
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,gutenprint))
