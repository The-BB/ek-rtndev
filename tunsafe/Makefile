# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2020-2024 Entware
#
# Abandoned in 2018

include $(TOPDIR)/rules.mk

PKG_NAME:=tunsafe
PKG_VERSION:=1.5_rc2
PKG_RELEASE:=1


PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=85a871c1d226956df7c1308a1e5527556fe35fe1
PKG_SOURCE_URL:=https://github.com/TunSafe/TunSafe.git
PKG_MIRROR_HASH:=2e2a7341453783d8c4ba0e13c252c044029567ec5cfa84b981667113a2e90ee7

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/tunsafe
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=VPN
	DEPENDS:=+libstdcpp +(mips||mipsel):libatomic
	TITLE:=TunSafe
	URL:=https://www.tunsafe.com/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/tunsafe/description
 A high performance and secure VPN client that uses the WireGuard protocol.
 TunSafe makes it extremely simple to setup blazingly fast and secure VPN
 tunnels between Windows and Linux. This is a user-mode implementation that
 also supports non-standard obfuscation and TCP mode.
endef

ifeq ($(ARCH),arm)
TUNSAFE_EXTRA_FILES+= \
	crypto/chacha20/chacha20-arm-linux.S \
	crypto/poly1305/poly1305-arm-linux.S
else ifeq ($(ARCH),x86_64)
TUNSAFE_EXTRA_FILES+= \
	crypto/aesgcm/aesni_gcm-x64-linux.s \
	crypto/aesgcm/aesni-x64-linux.s \
	crypto/aesgcm/ghash-x64-linux.s \
	crypto/poly1305/poly1305-x64-linux.s \
	crypto/chacha20/chacha20-x64-linux.s
else
TUNSAFE_EXTRA_CFLAGS+=-DCHACHA20_WITH_ASM=0 -DBLAKE2S_WITH_ASM=0
endif

ifeq ($(or $(CONFIG_mips),$(CONFIG_mipsel)),y)
TUNSAFE_EXTRA_LDFLAGS+=-latomic
endif

define Build/Compile
	cd $(PKG_BUILD_DIR) && $(TARGET_CXX) -I. -DNDEBUG -DWITH_NETWORK_BSD=1 \
	    $(TUNSAFE_EXTRA_CFLAGS) $(TARGET_CPPFLAGS) -pthread -lrt -std=c++11 \
	    $(TUNSAFE_EXTRA_LDFLAGS) $(TARGET_LDFLAGS) $(TUNSAFE_EXTRA_FILES) \
	    tunsafe_amalgam.cpp -o tunsafe;
endef

define Package/tunsafe/conffiles
/opt/etc/tunsafe/main.conf
endef

define Package/tunsafe/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tunsafe $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/tunsafe
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/installer/TunSafe.conf \
		$(1)/opt/etc/tunsafe/main.conf
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S30tunsafe $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,tunsafe))
