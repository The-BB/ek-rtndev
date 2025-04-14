# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

# XXX switch to fork

include $(TOPDIR)/rules.mk

PKG_NAME:=afpfs-ng
PKG_VERSION:=0.9.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/rdmark/afpfs-ng
PKG_MIRROR_HASH:=1c31075c3efc0c0b6d2c599cc7c255b3b97e208b27ad7f1beadbfbfbd98d9971

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk
include $(INCLUDE_DIR)/nls.mk

define Package/afpfs-ng
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Filesystem
	TITLE:=a client for Apple Filing Protocol
	URL:=https://github.com/simonvetter/afpfs-ng
	DEPENDS:=+libfuse +libgcrypt +libreadline +USE_GLIBC:libbsd $(ICONV_DEPENDS)
endef

define Package/afpfs-ng/description
 afpfs-ng is an Apple Filing Protocol client that will allow BSD, Linux
 and Mac OS X systems to access files exported from a Mac OS system with
 AFP over TCP.
endef

MESON_ARGS += -Dlibbsd=$(if $(CONFIG_USE_MUSL),false,true)

define Package/afpfs-ng/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/{afp{cmd,fsd,getstatus},mount_afpfs} \
			$(1)/opt/bin
	$(LN) mount_afpfs $(1)/opt/bin/afp_client
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libafpclient.so $(1)/opt/lib
endef

$(eval $(call BuildPackage,afpfs-ng))
