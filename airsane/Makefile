# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=airsane
PKG_VERSION:=0.4.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=776acdc8dce6c6834bded03e2741765ac4b9853a
PKG_SOURCE_URL:=https://github.com/SimulPiscator/AirSane.git
PKG_MIRROR_HASH:=f7b0e91b475b41ffd6cd41ff791c635c1251d54e7ac282e55f150a7b6b53718d

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
include $(INCLUDE_DIR)/nls.mk

define Package/airsane
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+libavahi-client +sane-libs
	TITLE:=AirScan Scanner publisher
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/airsane/description
 Publish SANE scanners to MacOS and Android via Apple AirScan.
endef

define Package/airsane/conffiles
/opt/etc/airsane/ignore.conf
/opt/etc/airsane/options.conf
/opt/etc/config/airsaned.conf
endef

# undefined reference to symbol '__atomic_store_8@@LIBATOMIC_1.0'
# error adding symbols: DSO missing from command line
ifeq ($(CONFIG_USE_MUSL),y)
TARGET_LDFLAGS += -latomic
endif

define Package/airsane/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/airsaned $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/airsane
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/airsane/*.conf $(1)/opt/etc/airsane
	$(INSTALL_DIR) $(1)/opt/etc/config
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/default/airsane $(1)/opt/etc/config/airsaned.conf
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) files/S43airsaned $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,airsane))
