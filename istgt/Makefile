# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# Abandoned in 2017

include $(TOPDIR)/rules.mk

PKG_NAME:=istgt
PKG_VERSION:=20150713
PKG_RELEASE:=4

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=14b0bacacedc9ac7e96fc34cf720800047f6194a
PKG_SOURCE_URL:=https://github.com/elastocloud/istgt
PKG_MIRROR_HASH:=e0266bac06198dffe1e0e9e0801b9e99013d26d94097bf9d4adc96344a52ca42

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/istgt
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Filesystem
	DEPENDS:=+libpthread +libevent2
	TITLE:=An iSCSI target implementation
	URL:=http://www.peach.ne.jp/archives/istgt/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/istgt/description
 This is a BSD Port of istgt, which  provides iSCSI target side protocol
 (refer to RFC3720 about iSCSI) and SPC-3 (SCSI Primary Commands - 3)
 based logical unit emulation.
endef

CONFIGURE_ARGS += \
	--with-mediadir=/opt/var

define Package/istgt/conffiles
/opt/etc/istgt/auth.conf
/opt/etc/istgt/istgt.conf
/opt/etc/istgt/istgtcontrol.conf
endef

define Package/istgt/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/istgt $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/istgtcontrol $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/istgt
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/istgt/{auth,istgt,istgt.large,istgtcontrol}.conf.sample \
		$(1)/opt/etc/istgt
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S13istgt $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,istgt))
