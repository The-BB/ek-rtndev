# PDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=fatrace
PKG_VERSION:=0.18.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/martinpitt/fatrace
PKG_MIRROR_HASH:=1e2430dccc6a8f2aeaad2de3331d347137ce556c6657fe38fd80e18871615f01

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

define Package/fatrace
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=report system wide file access events
	URL:=https://piware.de/2012/02/fatrace-report-system-wide-file-access-events/
endef

define Package/fatrace/description
 fatrace reports file access events from all running processes.
 Its main purpose is to find processes which keep waking up the disk
 unnecessarily and thus prevent some power saving.
endef

define Package/fatrace/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fatrace $(1)/opt/bin
endef

$(eval $(call BuildPackage,fatrace))
