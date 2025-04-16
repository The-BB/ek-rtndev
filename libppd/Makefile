# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=libppd
PKG_VERSION:=2.1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/OpenPrinting/libppd/tar.gz/refs/tags/$(PKG_VERSION)?
PKG_HASH:=6f728cce3fb5eb862dec63859a9b258ae04684bb63345c7aaf47100826ea1ee6

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=COPYING LICENSE

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/libppd/Default
  SUBMENU:=Printing
  TITLE:=OpenPrinting libppd
  URL:=https://openprinting.github.io/
endef

define Package/libppd
  $(call Package/libppd/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:= \
	+libcups +libcupsfilters +libjpeg-turbo +libpng +libstdcpp +zlib \
	$(ICONV_DEPENDS)
endef

define Package/libppd/description
  Library for handling PPD files and PostScript output.
endef

define Package/genstrings
  $(call Package/libppd/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE+= (GNU gettext message generator)
  DEPENDS+=+libppd
endef

define Package/genstrings/description
  genstrings - GNU gettext message generator for the libppd PPD Compiler.
endef

define Package/ppdc-utils
  $(call Package/libppd/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE+= (ppdc utilities)
  DEPENDS+=+libppd
endef

define Package/ppdc-utils/description
  ppdc utilities - to build PPD files from driver information files (*.drv).
endef

define Package/testppdfile
  $(call Package/libppd/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE+= (testppdfile utility)
  DEPENDS+=+libppd
endef

define Package/testppdfile/description
  testppdfile utility - to test correctness and integrity of PPD files.
endef

CONFIGURE_ARGS += \
	--disable-acroread \
	--disable-mutool \
	--disable-pdftocairo \
	--enable-genstrings \
	--enable-ppdc-utils \
	--enable-testppdfile \
	--with-cups-config=$(STAGING_DIR)/opt/bin/cups-config \
	--with-gs-path=/opt/bin/gs \
	--with-pdftops=gs \
	--with-pdftops-path=/opt/bin/gs

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/ppd $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libppd.{a,so*} $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/*.pc $(1)/opt/lib/pkgconfig
endef

define Package/libppd/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libppd.so* $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/ppdc $(1)/opt/share
endef

define Package/genstrings/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/genstrings $(1)/opt/bin
endef

define Package/ppdc-utils/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/ppd{c,html,i,merge,po} $(1)/opt/bin
endef

define Package/testppdfile/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/testppdfile $(1)/opt/bin
endef

$(eval $(call BuildPackage,libppd))
$(eval $(call BuildPackage,genstrings))
$(eval $(call BuildPackage,ppdc-utils))
$(eval $(call BuildPackage,testppdfile))
