# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=accel-ppp
PKG_VERSION:=1.12.0
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=6ce96d9d6eb3fa036d73aaf535784caddc7f3552
PKG_SOURCE_URL:=https://github.com/xebd/accel-ppp
PKG_MIRROR_HASH:=63eb3a5c63f102a227a4f6532950c2c0c766d31a8963afb213865829ffbeded2

CMAKE_BINARY_SUBDIR:=openwrt-build

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/accel-ppp
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=VPN
	DEPENDS:=+libopenssl +libpcre +USE_MUSL:libucontext
	TITLE:=accel-ppp VPN server
	URL:=https://accel-ppp.org/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/accel-ppp/description
 The ACCEL-PPP is high performance PPTP/L2TP/PPPoE server for Linux. Userspace
 daemon has its own PPP implementation, so it does not uses pppd and one process
 (multi-threaded) manages all connections.
endef

CMAKE_OPTIONS += \
	-DBUILD_DRIVER=FALSE \
	-DLIB_SUFFIX='' \
	-DLOG_PGSQL=FALSE \
	-DNETSNMP=FALSE \
	-DRADIUS=TRUE \
	-DSHAPER=FALSE

TARGET_CFLAGS += \
	-I$(STAGING_DIR)/opt/include

TARGET_LDFLAGS += \
	-Wl,-rpath,/opt/lib/accel-ppp

define Package/accel-ppp/conffiles
/opt/etc/accel-ppp.conf
endef

define Build/InstallDev
	true
endef

define Package/accel-ppp/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/accel-cmd $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/accel-pppd $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/lib/accel-ppp
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/lib/accel-ppp/lib*.so \
		$(1)/opt/lib/accel-ppp
	$(INSTALL_DIR) $(1)/opt/share/accel-ppp/l2tp
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/opt/share/accel-ppp/l2tp/dictionary* \
		$(1)/opt/share/accel-ppp/l2tp
	$(INSTALL_DIR) $(1)/opt/share/accel-ppp/radius
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/opt/share/accel-ppp/radius/dictionary* \
		$(1)/opt/share/accel-ppp/radius
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/accel-pppd/accel-ppp.conf $(1)/opt/etc
	$(INSTALL_BIN) files/S60accel-ppp $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/var/{lib,log}/accel-ppp
endef

$(eval $(call BuildPackage,accel-ppp))
