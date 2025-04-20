# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2015-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=perl-image-exiftool
PKG_VERSION:=13.27
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://exiftool.org
PKG_SOURCE:=Image-ExifTool-$(PKG_VERSION).tar.gz
PKG_HASH:=4b772e8766f8eb098ac8ab208fd80f7736bc65a23a1104511173709f48db43a4

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=Artistic-1.0-Perl GPL-1.0-or-later

PKG_BUILD_DIR:=$(BUILD_DIR)/perl/Image-ExifTool-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/perl/perlmod.mk

define Package/perl-image-exiftool
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=module for image data extraction
	URL:=https://exiftool.org/
	DEPENDS:=+perl +perlbase-base +perlbase-encode +perlbase-essential
	DEPENDS+=+perlbase-file +perlbase-time
endef

define Build/Configure
	$(call perlmod/Configure,,)
endef

define Build/Compile
	$(call perlmod/Compile,,)
endef

define Package/perl-image-exiftool/install
	$(call perlmod/Install,$(1),File Image Image/ExifTool auto/Image/ExifTool)
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/exiftool $(1)/opt/bin
	$(SED) 's,#!.*perl,#!/opt/bin/perl,' $(1)/opt/bin/exiftool
endef

$(eval $(call BuildPackage,perl-image-exiftool))
