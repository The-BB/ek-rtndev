# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# Based on https://github.com/FranciscoBorges/openwrt-printing-packages
# This is the last release with old PDF implementation

include $(TOPDIR)/rules.mk

PKG_NAME:=ghostscript
PKG_VERSION:=10.01.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/ArtifexSoftware/ghostpdl-downloads/releases/download/gs$(subst .,,$(PKG_VERSION))
PKG_HASH:=a4cd61a07fec161bee35da0211a5e5cde8ff8a0aaf942fc0176715e499d21661

PKG_BUILD_DEPENDS:=ghostscript/host
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/ghostscript
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+fontconfig +libidn +libtiff +libcups
	TITLE:=interpreter for the PostScript language and for PDF
	URL:=https://www.ghostscript.com/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/ghostscript/description
 An interpreter for the PostScript language and for PDF.
endef

GS_AUX_BINARIES:=echogs genarch genconf packps

HOST_CONFIGURE_ARGS += \
	--without-libtiff \
	--disable-contrib \
	--disable-fontconfig \
	--disable-dbus \
	--disable-cups \
	--disable-openjpeg \
	--disable-gtk \
	--with-libiconv=no \
	--without-libidn \
	--without-libpaper \
	--without-pdftoraster \
	--without-ijs \
	--without-jbig2dec \
	--without-urf \
	--without-tesseract \
	--without-x \
	--with-drivers=""

define Host/Compile
	$(foreach binary,$(GS_AUX_BINARIES),
		$(call Host/Compile/Default,obj/aux/$(binary))
	)
endef

define Host/Install
endef

CONFIGURE_ARGS += \
	--disable-compile-inits \
	--with-system-libtiff \
	--with-fontpath=/opt/share/fonts/ghostscript/fonts/:/opt/share/fonts/default/ghostscript/:/opt/share/fonts/default/TrueType/:/opt/share/fonts/default/Type1:/opt/share/cups/fonts/:/opt/share/fonts/ \

define Build/Configure
	(cd $(PKG_BUILD_DIR) && $(RM) -r jpeg leptonica libpng tesseract tiff zlib)
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
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/bin $(1)/opt
	$(CP) $(PKG_INSTALL_DIR)/opt/share/ghostscript $(1)/opt/share
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,ghostscript))
