#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=par2cmdline
PKG_VERSION:=0.8.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=9935dbf808cfc30f6e08e85645a70e38f555eba5
PKG_SOURCE_URL:=https://github.com/Parchive/par2cmdline
PKG_MIRROR_HASH:=d04173574630407186ec312e305e1029348bde6e3e0685a0d4c82372d97d4bbd

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/par2cmdline
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+libstdcpp
	TITLE:=file verification and repair tool
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/par2cmdline/description
 par2cmdline is a PAR 2.0 compatible file verification and repair tool.
endef

define Package/par2cmdline/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/par2 $(1)/opt/bin
	$(FIND) $(PKG_INSTALL_DIR)/opt/bin -type l -exec $(CP) -a {} $(1)/opt/bin \;
endef

$(eval $(call BuildPackage,par2cmdline))
