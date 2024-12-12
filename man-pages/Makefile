# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2017-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=man-pages
PKG_VERSION:=6.9.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://www.kernel.org/pub/linux/docs/man-pages
PKG_HASH:=3ae3f8ad97487d2c1b14258231d97d03b4e569b915377f6dd4f6be7141c57ee0

include $(INCLUDE_DIR)/package.mk

define Package/man-pages
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Linux man-pages
	DEPENDS:=+man-db
	URL:=http://www.kernel.org/pub/linux/docs/man-pages
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
