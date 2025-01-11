# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=accel-ppp
PKG_VERSION:=1.13.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/accel-ppp/accel-ppp
PKG_MIRROR_HASH:=f1e41a8bbc789777237727984c083eaa4a14a6d3db478e92816865ef05f16dfe

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
  ifneq ($(CONFIG_USE_MUSL),y)
	$(INSTALL_DIR) $(1)/opt/etc/ld.so.conf.d
	$(INSTALL_DATA) ./files/accel-ppp.conf $(1)/opt/etc/ld.so.conf.d
  endif
endef

ifeq ($(CONFIG_USE_MUSL),y)
define Package/accel-ppp/postinst
#!/bin/sh

if ! grep -q 'accel-ppp' /opt/etc/ld-musl-$(ARCH)$(if $(or $(CONFIG_mips),$(CONFIG_mipsel)),-sf).path; then
  printf "# path to accel-ppp libs\n/opt/lib/accel-ppp\n" >> \
  /opt/etc/ld-musl-$(ARCH)$(if $(or $(CONFIG_mips),$(CONFIG_mipsel)),-sf).path
fi
endef
endif

$(eval $(call BuildPackage,accel-ppp))
