# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=lcms
PKG_VERSION:=2.17
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)2-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)
PKG_HASH:=d11af569e42a1baa1650d20ad61d12e41af4fead4aa7964a01f93b08b53ab074

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)2-$(PKG_VERSION)

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

define Package/lcms
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Printing
  TITLE:=Color Management Library
  URL:=https://www.littlecms.com/
  DEPENDS:=+libjpeg-turbo +libtiff
endef

define Package/lcms/description
 Little CMS intends to be an OPEN SOURCE small-footprint color
 management engine, with special focus on accuracy and performance.
endef

define Package/lcms/config
if PACKAGE_lcms
comment "Optional features"

	config LCMS2_PLUGIN_FASTFLOAT
		bool "Enable fast float plugin"
		help
			Build and install the fast float plugin.

	config LCMS2_PLUGIN_MULTITHREADED
		bool "Enable multi threaded plugin"
		help
			Build and install the multi threaded plugin.
endif
endef

MESON_ARGS += \
	-Dtests=disabled \
	-Dfastfloat=$(if $(CONFIG_LCMS2_PLUGIN_FASTFLOAT),true,false) \
	-Dthreaded=$(if $(CONFIG_LCMS2_PLUGIN_MULTITHREADED),true,false) \
	-Dutils=true

define Package/lcms/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/*icc $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblcms2.so* $(1)/opt/lib
  ifneq ($(CONFIG_LCMS2_PLUGIN_FASTFLOAT),)
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblcms2_fast_float.so* $(1)/opt/lib
  endif
  ifneq ($(CONFIG_LCMS2_PLUGIN_MULTITHREADED),)
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblcms2_threaded.so* $(1)/opt/lib
  endif
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/lcms2*.h $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblcms2.{a,so*} $(1)/opt/lib
  ifneq ($(CONFIG_LCMS2_PLUGIN_FASTFLOAT),)
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblcms2_fast_float.{a,so*} $(1)/opt/lib
  endif
  ifneq ($(CONFIG_LCMS2_PLUGIN_MULTITHREADED),)
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/liblcms2_threaded.{a,so*} $(1)/opt/lib
  endif
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/lcms2.pc $(1)/opt/lib/pkgconfig
endef

$(eval $(call BuildPackage,lcms))
