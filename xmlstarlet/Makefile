# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# Abandoned in 2018

include $(TOPDIR)/rules.mk

PKG_NAME:=xmlstarlet
PKG_VERSION:=1.6.1
PKG_RELEASE:=3

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=4ad40171da05c4f7a01c367dfefe0bb188008899
PKG_SOURCE_URL:=https://git.code.sf.net/p/xmlstar/code
PKG_MIRROR_HASH:=9ac2b067f39adc5e92b35a44661c671bfca35425a9ea90980916621989599058

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/xmlstarlet
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+libexslt
	TITLE:=command line XML toolkit
	URL:=https://xmlstar.sourceforge.net/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/xmlstarlet/description
 XMLStarlet is a set of command line utilities (tools) which can be used
 to transform, query, validate, and edit XML documents and files using simple
 set of shell commands in similar way it is done for plain text files using
 UNIX grep, sed, awk, diff, patch, join, etc commands.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(SED) "s|git describe --tags --dirty|echo $(PKG_VERSION)|g" $(PKG_BUILD_DIR)/configure.ac
	$(SED) "s|git describe --tags --dirty|echo $(PKG_VERSION)|g" $(PKG_BUILD_DIR)/Makefile.am
endef

CONFIGURE_ARGS += \
	--disable-build-docs \
	--with-libxml-include-prefix="$(STAGING_DIR)/opt/include/libxml2" \
	--with-libxml-libs-prefix="$(STAGING_DIR)/opt/lib" \
	--with-libxslt-include-prefix="$(STAGING_DIR)/opt/include/libxslt" \
	--with-libxslt-libs-prefix="$(STAGING_DIR)/opt/lib" \

define Package/xmlstarlet/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/xml $(1)/opt/bin
endef

$(eval $(call BuildPackage,xmlstarlet))
