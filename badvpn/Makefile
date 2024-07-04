# SPDX-License-Identifier: BSD-3-Clause
#
# Copyright (C) 2017-2024 Entware
#
# ported to Entware from https://github.com/helmiau/badvpn_corkscrew
# Project archieved

include $(TOPDIR)/rules.mk

PKG_NAME:=badvpn
PKG_VERSION:=1.999.133
PKG_RELEASE=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=07268f02706e78e282e19641b5d1d41e8e89bf31
PKG_SOURCE_URL:=https://github.com/ambrop72/badvpn.git
PKG_MIRROR_HASH:=ca982200a9458e5d15dd5f3c9cefc80bd5eca4a76b6858577b6be248339e4f2b

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=BadVPN
	SUBMENU:=VPN
endef

define Package/$(PKG_NAME)/description
 The tun2socks program "socksifes" TCP connections at the network layer.
 It implements a TUN device which accepts all incoming TCP connections (regardless of destination IP),
 and forwards the connections through a SOCKS server. This allows you to forward all connections through SOCKS,
 without any need for application support. It can be used, for example, to forward connections through a remote SSH server.
endef

CMAKE_OPTIONS += \
		-DBUILD_NOTHING_BY_DEFAULT=1 \
		-DBUILD_TUN2SOCKS=1 \
		-DBUILD_UDPGW=1

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/badvpn-tun2socks $(1)/opt/bin/badvpn-tun2socks
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/badvpn-udpgw $(1)/opt/bin/badvpn-udpgw
endef

$(eval $(call BuildPackage,badvpn))
