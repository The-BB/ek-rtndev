#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ioping
PKG_VERSION:=1.3
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=d52efa35e1d6d02495434e9447ee04c21b2e1010
PKG_SOURCE_URL:=https://github.com/koct9i/ioping.git
PKG_MIRROR_HASH:=6dceafa52e8f449485a0f17ac88284d627306a70887f2b0df1e93b255373ebaa

include $(INCLUDE_DIR)/package.mk

define Package/ioping
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=simple disk I/0 latency measuring tool
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/ioping/description
 A tool to monitor I/O latency in real time. It shows disk latency in the same
 way as ping shows network latency.
endef

define Package/ioping/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ioping $(1)/opt/bin
endef

$(eval $(call BuildPackage,ioping))
