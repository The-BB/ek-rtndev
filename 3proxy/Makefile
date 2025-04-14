# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=3proxy
PKG_VERSION:=0.9.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/z3APA3A/3proxy
PKG_MIRROR_HASH:=7a6134f34555fbe63bf38ac0d26e8f92074d43dd229472e91b75eb815f774e2c

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=copying

include $(INCLUDE_DIR)/package.mk

define Package/3proxy
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Web Servers/Proxies
	TITLE:=tiny free proxy server
	URL:=https://3proxy.org/
endef

define Package/3proxy/description
 3proxy is universal proxy server. It can be used to provide internal users
 with fully controllable access to external resources or to provide external
 users with access to internal resources.
 Note: SSL plugin requires libopenssl to be installed.
endef

define Package/3proxy/conffiles
/opt/etc/3proxy/3proxy.cfg
/opt/etc/3proxy/bandlimiters
/opt/etc/3proxy/counters
/opt/etc/3proxy/passwd
endef

MAKE_FLAGS += -f Makefile.Linux

define Package/3proxy/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_BUILD_DIR)/bin/{3proxy,ftppr,mycrypt,pop3p,proxy,smtpp,socks,tcppm,tlspr,udppm} \
		$(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib/3proxy
	$(INSTALL_BIN) \
		$(PKG_BUILD_DIR)/bin/{PCRE,Strings,Traffic,Transparent}Plugin.ld.so \
		$(1)/opt/lib/3proxy
	$(INSTALL_DIR) $(1)/opt/etc/3proxy
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/scripts/3proxy.cfg $(1)/opt/etc/3proxy
	touch $(1)/opt/etc/3proxy/{passwd,counters,bandlimiters}
	chmod 0600 $(1)/opt/etc/3proxy/*
	$(CP) $(PKG_BUILD_DIR)/scripts/add3proxyuser.sh $(1)/opt/etc/3proxy
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S23proxy $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,3proxy))
