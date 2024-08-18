#
# Copyright (C) 2017-2024 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=man-pages
PKG_VERSION:=6.9
PKG_RELEASE:=2

PKG_SOURCE_URL:=https://www.kernel.org/pub/linux/docs/man-pages
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=9508887dccbb7e77e42532a0bb7af18400769c78a5b9d13b2f982e579e0e2752

include $(INCLUDE_DIR)/package.mk

define Package/man-pages
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=unix manual pages
	DEPENDS:=+man-db
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/man-pages/description
 Linux kernel and C library user-space interface documentation.
endef

define Build/Compile
endef

define Package/man-pages/install
	$(INSTALL_DIR) $(1)/opt/share/man
	$(CP) $(PKG_BUILD_DIR)/man/man[1-8]* $(1)/opt/share/man
endef

define Package/man-pages/postinst
#!/bin/sh

### colors
ansi_red="\033[1;31m"
ansi_blue="\033[1;34m"
ansi_white="\033[1;37m"
ansi_std="\033[0m"

printf "\n$$ansi_blue %s $$ansi_white %s $$ansi_std" "Info:" "creating man database ..."
if ! mandb -cq > /dev/null 2>&1 ; then
  printf "$$ansi_red %s $$ansi_std\n\n" "faild"
else
  printf "$$ansi_white %s $$ansi_std\n\n" "done"
fi
endef

$(eval $(call BuildPackage,man-pages))
