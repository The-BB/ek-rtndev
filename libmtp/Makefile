# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=libmtp
PKG_VERSION:=1.1.22
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/libmtp/libmtp
PKG_MIRROR_HASH:=80a9e54597ce734bc447fb177d0d5c89fcb4f3a80c2d489242ea791966fbfaa3

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=LGPL-2.1-only
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/libmtp/Default
	SUBMENU:=Filesystem
	URL:=https://libmtp.sourceforge.net/
endef

define Package/libmtp
	$(call Package/libmtp/Default)
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=a library to access MTP devices
	DEPENDS:=+libgcrypt +libusb-1.0 $(ICONV_DEPENDS)
endef

define Package/libmtp-utils
	$(call Package/libmtp/Default)
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=libmtp utilities
	DEPENDS:=+libmtp
endef

define Package/libmtp/description
 libmtp implements an MTP initiator, which means it initiate MTP
 sessions with devices. The devices responding are known as MTP responders.
 libmtp runs on something with a USB host controller interface, using libusb
 to access the host controller.
endef

define Package/libmtp-utils/description
 Media Transfer Protocol (MTP) library tools.
endef

CONFIGURE_ARGS += \
	--with-libiconv-prefix=$(ICONV_PREFIX) \
	--with-udev=/opt/lib/udev \
	--disable-configfiles

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/libmtp.h $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libmtp.{a,so*} $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libmtp.pc $(1)/opt/lib/pkgconfig
endef

define Package/libmtp/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libmtp.so* $(1)/opt/lib
endef

define Package/libmtp-utils/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/mtp-* $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib/udev
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/udev/mtp-probe $(1)/opt/lib/udev
endef

$(eval $(call BuildPackage,libmtp))
$(eval $(call BuildPackage,libmtp-utils))
