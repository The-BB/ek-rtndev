#
# Copyright (C) 2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libcryptopp
PKG_VERSION:=8.8.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=4d0cad5401d1a2c998b314bc89288c9620d3021d
PKG_SOURCE_URL:=https://github.com/weidai11/cryptopp.git
PKG_MIRROR_HASH:=a1919ed68fb9ac5571bd6b20113cdb5742ee12b8c325ff05cd9f4d7b43d17e7e

PKG_CONFIG_DEPENDS:= \
	CONFIG_LIBCRYPTOPP_TESTSUITE

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libcryptopp
	SECTION:=libs
	CATEGORY:=Libraries
	DEPENDS:=+libstdcpp
	TITLE:=C++ class library of cryptographic schemes
	URL:=https://www.cryptopp.com/
endef

define Package/libcryptopp/description
 Crypto++ Library is a free C++ class library of cryptographic schemes.
endef

define Package/libcryptopp/config
	config LIBCRYPTOPP_TESTSUITE
		depends on PACKAGE_libcryptopp
		bool "Add native test suite"
endef

MAKE_VARS += \
	PREFIX=/opt \
	PC_PREFIX=/opt \
	HAS_SOLIB_VERSION=1 \
	LINK_LIBRARY="libcryptopp.a libcryptopp.so"

TARGET_CPPFLAGS += -DCRYPTOPP_DISABLE_ASM

TARGET_CXXFLAGS += $(FPIC)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/cryptopp $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/libcryptopp.{a,so*} $(1)/opt/lib
endef

define Package/libcryptopp/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcryptopp.so* $(1)/opt/lib
ifeq ($(CONFIG_LIBCRYPTOPP_TESTSUITE),y)
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/cryptest.exe $(1)/opt/bin
	$(INSTALL_BIN) files/cryptest.sh $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/cryptopp $(1)/opt/share
endif
endef

$(eval $(call BuildPackage,libcryptopp))
