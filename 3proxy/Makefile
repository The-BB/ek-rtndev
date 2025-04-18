#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=3proxy
PKG_VERSION:=0.9.4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=346880eb2e73836385e5f7648f738efcece580ac
PKG_SOURCE_URL:=https://github.com/z3APA3A/3proxy
PKG_MIRROR_HASH:=2dab73b73dcfbd6e0aa55393a2e72bb1552b49c88e4da00ea43f92445ba1bfd5

include $(INCLUDE_DIR)/package.mk

define Package/3proxy
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Web Servers/Proxies
	DEPENDS:=+libpthread
	TITLE:=3proxy free proxy server
	URL:=http://www.3proxy.ru
	MAINTAINER:=Entware team, https://entware.net
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

define Build/Configure
	$(CP) $(PKG_BUILD_DIR)/Makefile.Linux $(PKG_BUILD_DIR)/Makefile
endef

define Package/3proxy/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_BUILD_DIR)/bin/{3proxy,ftppr,mycrypt,pop3p,proxy,smtpp,socks,tcppm,udppm} \
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
