# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=rdfind
PKG_VERSION:=1.7.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=releases/$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/pauldreik/rdfind
PKG_MIRROR_HASH:=56ca59abf90830ae598378dd3c3bde5ef6d959bdc9eb506af82848ed10cd0907

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING LICENSE

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/rdfind
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=find duplicate files utility
  URL:=https://rdfind.pauldreik.se/
  DEPENDS:=+libnettle +libstdcpp +libxxhash
endef

define Package/rdfind/description
 Rdfind is a command line tool that finds duplicate files. It is
 useful for compressing backup directories or just finding duplicate files.
 It compares files based on their content, NOT on their file names.
endef

TARGET_CXXFLAGS += -std=c++17

define Package/rdfind/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/rdfind $(1)/opt/bin
endef

$(eval $(call BuildPackage,rdfind))
