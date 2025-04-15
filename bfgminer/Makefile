# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=bfgminer
PKG_VERSION:=5.5.0
PKG_RELEASE:=5

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/luke-jr/bfgminer
PKG_MIRROR_HASH:=c4c737d7b8bedc43ac5523b65d14bd5249da037f2126d1ef1f3bb9c529fd9622

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/bfgminer
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=modular ASIC/FPGA Bitcoin miner
  URL:=http://bfgminer.org/
  DEPENDS:=+jansson +libcurl +libevent2 +libevent2-pthreads +libncursesw +libusb-1.0		
endef

define Package/bfgminer/description
 This is a multi-threaded multi-pool GPU, FPGA and CPU miner with ATI
 GPU monitoring, (over)clocking and fanspeed support for bitcoin and derivative
 coins.
endef

UTHASH_VER:=2.3.0
UTHASH_FILE:=uthash-$(UTHASH_VER).tar.gz
define Download/uthash
  FILE:=$(UTHASH_FILE)
  URL:=https://codeload.github.com/troydhanson/uthash/tar.gz/refs/tags/v$(UTHASH_VER)?
  HASH:=e10382ab75518bad8319eb922ad04f907cb20cccb451a3aa980c9d005e661acc
endef

CONFIGURE_ARGS += \
	--enable-cpumining \
	--enable-keccak \
	--enable-scrypt \
	--with-curses=ncurses \
	--with-udevrulesdir=/opt/lib/udev/rules.d \
	--without-libmicrohttpd \
	--without-libudev \
	--without-sensors \
	--without-system-libbase58 \
	--without-uio \
	--without-vfio

TARGET_CFLAGS += \
	-std=gnu99 \
	-Iuthash-$(UTHASH_VER)/src \
	-DJSON_INTEGER_IS_LONG_LONG

define Build/Prepare
	$(call Build/Prepare/Default)
	$(HOST_TAR) -xzf $(DL_DIR)/$(UTHASH_FILE) -C $(PKG_BUILD_DIR)
	$(SED) 's,"PACKAGE_VERSION"-unknown,$(PKG_SOURCE_VERSION),' \
		$(PKG_BUILD_DIR)/gen-version.sh
endef

define Package/bfgminer/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/bfgminer{,-rpc} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/libbase58.so* \
		$(PKG_INSTALL_DIR)/opt/lib/libblkmaker-0.1.so* \
		$(PKG_INSTALL_DIR)/opt/lib/libblkmaker_jansson-0.1.so* \
			$(1)/opt/lib
endef

$(eval $(call Download,uthash))
$(eval $(call BuildPackage,bfgminer))
