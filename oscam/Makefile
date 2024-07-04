# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware
#
# Streamboard/OScam Repository has been migrated to GitLab
# https://svn.streamboard.tv/oscam/tags/1.20@11745

include $(TOPDIR)/rules.mk

PKG_NAME:=oscam
PKG_VERSION:=1.20
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=fd15b442ae0e38814f24543e663d2dcad6516e7d
PKG_SOURCE_URL:=https://git.streamboard.tv/common/oscam
PKG_MIRROR_HASH:=b542102d651832d8afbdcd005e2218088eb58bdb4b8d54a23d94427e9871a5fd

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/oscam
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libpcsclite +libopenssl
	TITLE:=CAM software
	URL:=https://wiki.streamboard.tv/wiki/OSCam/en
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/oscam/description
 OSCam is an Open Source Conditional Access Module software, based on the very
 good MpCS version 0.9d.
endef

define Package/oscam/conffiles
/opt/etc/oscam/
endef

CMAKE_OPTIONS += \
	-DCS_CONFDIR=/opt/etc/oscam \
	-DLIBUSBDIR=$(STAGING_DIR)/opt \
	-DOPTIONAL_INCLUDE_DIR=$(STAGING_DIR)/opt/include \
	-DOPTIONAL_LINK_DIR=$(STAGING_DIR)/opt/lib \
	-DOPENSSL_INCLUDE_DIR=$(STAGING_DIR)/opt/include \
	-DWITH_SSL=1 \
	-DHAVE_LIBCRYPTO=1

define Build/InstallDev
	true
endef

define Package/oscam/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/oscam $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/oscam
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/share/doc/oscam/example/* $(1)/opt/etc/oscam
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S59oscam $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/var/log/oscam/cw
endef

$(eval $(call BuildPackage,oscam))
