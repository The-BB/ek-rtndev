# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# Abandoned in 2018

include $(TOPDIR)/rules.mk

PKG_NAME:=microdc2
PKG_REAL_VERSION:=0.15.6
PKG_RELEASE:=3

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2018-07-18
PKG_SOURCE_VERSION:=9343cf76972f4f16ac1782788933589e72be63b7
PKG_SOURCE_URL:=https://github.com/19h/microdc2
PKG_MIRROR_HASH:=ea1fa944315f3c6ed51347f6ad8877f794573b5f158ba0a1b9ee4be6ee76b1b9

PKG_VERSION:=$(PKG_REAL_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/microdc2
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=P2P
	TITLE:=command-line based Direct Connect client
	URL:=$(PKG_SOURCE_URL)
	DEPENDS:=+libbz2 +libncurses +libreadline +libxml2 $(INTL_DEPENDS)
endef

define Package/microdc2/description
 A command-line based Direct Connect client.
endef

MAKE_FLAGS += \
	LTLIBICONV=""

define Package/microdc2/conffiles
/opt/share/microdc2/config
endef

define Package/microdc2/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/microdc2 $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/share/microdc2
	$(INSTALL_CONF) ./files/microdc2.conf $(1)/opt/share/microdc2/config
endef

$(eval $(call BuildPackage,microdc2))
