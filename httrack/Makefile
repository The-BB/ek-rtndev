# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2017-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=httrack
PKG_VERSION:=3.49.6
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=748c35de7858ead963daf1393ad023d75b7820c2
PKG_SOURCE_URL:=https://github.com/xroche/httrack
PKG_MIRROR_HASH:=810956f91ecf2790368304ef8e3be54e01975eb4b71b55d75d3a9b3934282ea4

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_FLAGS:=no-mips16
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/httrack
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=File Transfer
  TITLE:=website copier
  URL:=https://www.httrack.com/
  DEPENDS:=+libopenssl
endef

define Package/httrack/description
 HTTrack is a free and easy-to-use offline browser utility.
 It allows you to download a WWW site from the Internet to a local directory,
 building recursively all directories, getting HTML, images, and other files
 from the server to your computer. HTTrack arranges the original site's relative
 link-structure.
endef

CONFIGURE_ARGS += \
	--with-zlib="$(STAGING_DIR)/opt"

TARGET_LDFLAGS += $(if $(CONFIG_GCC_LIBSSP),-lssp)

define Package/httrack/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/{htsserver,httrack,proxytrack} \
		$(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib/httrack
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/httrack/*.so* \
		$(1)/opt/lib/httrack
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/*.so* \
		$(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/share/httrack/html
	$(CP) $(PKG_INSTALL_DIR)/opt/share/httrack/{lang{,.def,.indexes},templates} \
		$(1)/opt/share/httrack
	$(CP) $(PKG_INSTALL_DIR)/opt/share/doc/httrack/* \
		$(1)/opt/share/httrack/html
endef

$(eval $(call BuildPackage,httrack))
