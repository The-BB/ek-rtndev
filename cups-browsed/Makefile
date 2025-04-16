# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=cups-browsed
PKG_VERSION:=2.1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/OpenPrinting/cups-browsed/tar.gz/refs/tags/$(PKG_VERSION)?
PKG_HASH:=82153a65c6365ab7b9d92128c280156c9094cdad3c8da93794b83abe5e7ca181

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=COPYING LICENSE

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/cups-browsed
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Printing
  TITLE:=OpenPrinting bonjour remote printer browsing daemon
  URL:=https://openprinting.github.io/
  DEPENDS:= \
	+glib2 +libavahi-client +libavahi-dbus-support +libavahi-glib \
	+libcups +libcupsfilters +libjpeg-turbo +libpng +libppd +zlib \
	$(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

define Package/cups-browsed/description
 cups-browsed - a daemon for browsing the Bonjour broadcasts of
 shared, remote CUPS printers.
endef

define Package/cups-browsed/conffiles
/opt/etc/cups/cups-browsed.conf
endef

CONFIGURE_ARGS += \
	--with-cups-config=$(STAGING_DIR)/opt/bin/cups-config \
	--with-rcdir=/opt/etc

define Package/cups-browsed/install
	$(INSTALL_DIR) $(1)/opt/etc/cups
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/etc/cups/cups-browsed.conf \
		$(1)/opt/etc/cups
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S82cups-browsed $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/lib/cups/backend
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/cups/backend/implicitclass \
		$(1)/opt/lib/cups/backend
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/cups-browsed $(1)/opt/sbin
endef

$(eval $(call BuildPackage,cups-browsed))
