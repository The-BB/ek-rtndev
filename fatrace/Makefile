#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fatrace
PKG_VERSION:=0.17.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=43327b194d995df56ab1c447366169cbf3a26c13
PKG_SOURCE_URL:=https://github.com/martinpitt/fatrace.git
PKG_MIRROR_HASH:=d7404ad591acc7c07674f9545d1141b666a9bd6db422fec0cbb74e5cf5443337

include $(INCLUDE_DIR)/package.mk

define Package/fatrace
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=fatrace reports file access events from all running processes
	URL:=https://piware.de/2012/02/fatrace-report-system-wide-file-access-events/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/fatrace/description
 Its main purpose is to find processes which keep waking up the disk unnecessarily
 and thus prevent some power saving.
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) -c $(TARGET_CPPFLAGS) -o $(PKG_BUILD_DIR)/$(PKG_NAME).o $(PKG_BUILD_DIR)/$(PKG_NAME).c
	$(TARGET_CC) $(TARGET_LDFLAGS) -L$(STAGING_DIR)/opt/lib -o $(PKG_BUILD_DIR)/$(PKG_NAME) $(PKG_BUILD_DIR)/$(PKG_NAME).o
endef

define Package/fatrace/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fatrace $(1)/opt/bin
endef

$(eval $(call BuildPackage,fatrace))
