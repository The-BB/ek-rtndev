# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

# Based on https://github.com/FranciscoBorges/openwrt-printing-packages

include $(TOPDIR)/rules.mk

PKG_NAME:=ghostscript
PKG_VERSION:=10.05.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=ghostpdl-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/ArtifexSoftware/ghostpdl
PKG_MIRROR_HASH:=606c65c9f159d5bbf2be0ca7d9ff3b49bd567dcfcfc85357d97bb04bb0ef7a17

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=AGPL-3.0-only
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=ghostscript/host
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/ghostscript
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Printing
  TITLE:=interpreter for the PostScript language and for PDF
  URL:=https://www.ghostscript.com/
  DEPENDS:= \
	+fontconfig +lcms +libarchive +libcups +libexpat +libfreetype +libidn \
	+libjpeg-turbo +libleptonica +libpng +libstdcpp +libtiff +tesseract \
	+zlib $(ICONV_DEPENDS)
endef

define Package/ghostscript/description
 An interpreter for the PostScript language and for PDF.
endef

GS_AUX_BINARIES:=echogs genarch genconf packps

HOST_CONFIGURE_ARGS += \
	--disable-contrib \
	--disable-cups \
	--disable-dbus \
	--disable-fontconfig \
	--disable-gtk \
	--disable-openjpeg \
	--with-drivers="" \
	--with-libiconv=no \
	--without-ijs \
	--without-jbig2dec \
	--without-libidn \
	--without-libpaper \
	--without-libtiff \
	--without-pdftoraster \
	--without-tesseract \
	--without-urf \
	--without-x

define Host/Compile
	$(foreach binary,$(GS_AUX_BINARIES),
		$(call Host/Compile/Default,obj/aux/$(binary))
	)
endef

define Host/Install
endef

CONFIGURE_ARGS += \
	--disable-compile-inits \
	--with-fontpath=/opt/share/fonts/default/TrueType/:/opt/share/fonts/default/Type1:/opt/share/cups/fonts/:/opt/share/fonts/ \
	CUPSCONFIG=$(STAGING_DIR)/opt/bin/cups-config \
	PKGCONFIG=$(STAGING_DIR_HOST)/bin/pkg-config

RM_DIRS:=expat freetype jpeg lcms2mt leptonica libpng tesseract tiff zlib

# warning: libarchive.so.20, needed by .../lib/libtesseract.so, not found (try using -rpath or -rpath-link)
TARGET_LDFLAGS += -larchive

define Build/Configure
	( cd $(PKG_BUILD_DIR) && rm -fr $(RM_DIRS); )
	$(call Build/Configure/Default)
	mkdir -p $(PKG_BUILD_DIR)/obj/aux
	for binary in $(GS_AUX_BINARIES); do \
		$(CP) $(HOST_BUILD_DIR)/obj/aux/$$$${binary} \
			$(PKG_BUILD_DIR)/obj/aux/$$$${binary}; \
		touch $(PKG_BUILD_DIR)/obj/aux/$$$${binary}; \
	done
endef

define Build/Install
	$(call Build/Install/Default)
	$(call Build/Install/Default,install-examples)
endef

define Package/ghostscript/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/ghostscript $(1)/opt/share
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,ghostscript))
