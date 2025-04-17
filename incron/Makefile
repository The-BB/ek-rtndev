# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

# XXX switch to fork

include $(TOPDIR)/rules.mk

PKG_NAME:=incron
PKG_VERSION:=0.5.17
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/dpvpro/incron-next
PKG_MIRROR_HASH:=125e1ffdaaa23342af76e1aadc7a0cbb174b0714756df1bdc9a7fefdf98a2353

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only LGPL-2.1-only MIT
PKG_LICENSE_FILES:=COPYING LICENSE-GPL LICENSE-LGPL LICENSE-X11

include $(INCLUDE_DIR)/package.mk

define Package/incron
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Filesystem
  TITLE:=cron-like daemon which handles filesystem events
  URL:=https://inotify.aiken.cz/
  DEPENDS:=+libstdcpp
endef

define Package/incron/description
 This program is the "inotify cron" system.
 You can use it a similar way as the regular cron. The difference is that the
 inotify cron handles filesystem events rather than time periods.
endef

define Package/incron/conffiles
/opt/etc/incron.conf
endef

define Package/incron/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/incrontab $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/incrond $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/incron.d
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/incron.conf.example $(1)/opt/etc/incron.conf
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S12incron $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,incron))
