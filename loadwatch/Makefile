# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2021 Entware

# Abandoned in 2003

include $(TOPDIR)/rules.mk

PKG_NAME:=loadwatch
PKG_VERSION:=1.1_alpha1
PKG_RELEASE:=6

PKG_SOURCE:=$(PKG_NAME)_1.0+$(subst 1_a,1a,$(PKG_VERSION)).orig.tar.gz
PKG_SOURCE_URL:=@DEBIAN/pool/main/l/loadwatch
PKG_HASH:=2a2044346ed980b4eed971494e7a9c088e8473daf0f153db8e4469e2d9a072a9

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-1.1

include $(INCLUDE_DIR)/package.mk

define Package/loadwatch
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=CPU tools
	TITLE:=run processes only at acceptable system load
	URL:=http://loadwatch.sourceforge.net
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/loadwatch/description
 loadwatch allows one or more processes to run only when the load on a machine is within
 certain bounds. The child processes are sent SIGSTOP when the machines load passes
 the high load mark. The processes are sent SIGCONT only after the machines load drops
 below the low load mark. The load is checked at a user definable interval.
endef

define Package/loadwatch/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/{loadwatch,lw-ctl} $(1)/opt/bin
endef

$(eval $(call BuildPackage,loadwatch))
