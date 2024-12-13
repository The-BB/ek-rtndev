# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PECL_NAME:=gmagick
PECL_LONGNAME:=Provides a wrapper to the GraphicsMagick library

PKG_REAL_VERSION:=2.0.6RC1
PKG_VERSION:=$(subst RC,_rc,$(PKG_REAL_VERSION))
PKG_RELEASE:=1

PKG_NAME:=php8-pecl-$(PECL_NAME)
PKG_SOURCE:=$(PECL_NAME)-$(PKG_REAL_VERSION).tgz
PKG_SOURCE_URL:=http://pecl.php.net/get/
PKG_HASH:=350cb71a4fbd58e037c7182cafa14e6f6df952126869205918fcc9ec5798e2fa

PKG_BUILD_DIR:=$(BUILD_DIR)/pecl-php8/$(PECL_NAME)-$(PKG_REAL_VERSION)

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=PHP-3.01
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(TOPDIR)/feeds/packages/lang/php8/pecl.mk

CONFIGURE_VARS += \
	WAND_BINARY=$(STAGING_DIR_ROOT)/opt/bin/GraphicsMagick-config

TARGET_CPPFLAGS += \
	-I$(STAGING_DIR)/opt/include/GraphicsMagick

$(eval $(call PHP8PECLPackage,$(PECL_NAME),$(PECL_LONGNAME),+graphicsmagick))
$(eval $(call BuildPackage,$(PKG_NAME)))
