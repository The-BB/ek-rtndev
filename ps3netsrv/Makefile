# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

# switch to using ps3netsrv_*.zip archive (3.5 MB vs 100+ MB)

include $(TOPDIR)/rules.mk

PKG_NAME:=ps3netsrv
PKG_REAL_VERSION:=1.47.48
PKG_VERSION:=20250126
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).zip
PKG_SOURCE_URL:=https://github.com/aldostools/webMAN-MOD/releases/download/$(PKG_REAL_VERSION)
PKG_HASH:=b2a88870c92455ab8242bbdb67b73c1924f8c8d57c32ec43c84cdec280e6cf1a

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(basename $(PKG_SOURCE))

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE.TXT

include $(INCLUDE_DIR)/package.mk

define Package/ps3netsrv/Default
  SECTION:=net
  CATEGORY:=Network
  TITLE:=C++ implementation of the ps3netsrv server
  URL:=https://aldostools.github.io/webMAN-MOD/
  DEPENDS:=+libstdcpp
endef

define Package/ps3netsrv
  $(call Package/ps3netsrv/Default)
  VARIANT:=nossl
  TITLE+= (no SSL)
endef

define Package/ps3netsrv-mbedtls
  $(call Package/ps3netsrv/Default)
  VARIANT:=mbedtls
  TITLE+= (Mbed TLS)
  DEPENDS+=+libmbedtls
endef

define Package/ps3netsrv/description
 ps3netsrv is a server application used to stream content from a
 remote server to the PS3.
endef

Package/ps3netsrv-mbedtls/description=$(Package/ps3netsrv/description)

MAKE_PATH:=$(PKG_NAME)
MAKE_FLAGS+=-f Makefile.linux

ifeq ($(BUILD_VARIANT),nossl)
	TARGET_CFLAGS += -DNOSSL
endif

ifeq ($(BUILD_VARIANT),mbedtls)
	TARGET_LDFLAGS += -lmbedtls -lmbedcrypto
endif

define Package/ps3netsrv/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(MAKE_PATH)/ps3netsrv $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S76ps3netsrv $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/share/ps3netsrv/{GAMES,PS3ISO}
endef

Package/ps3netsrv-mbedtls/install=$(Package/ps3netsrv/install)

$(eval $(call BuildPackage,ps3netsrv))
$(eval $(call BuildPackage,ps3netsrv-mbedtls))
