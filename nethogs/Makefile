# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=nethogs
PKG_VERSION:=0.8.8
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/raboof/nethogs
PKG_MIRROR_HASH:=2313cc36f7d1bdf8126ee314817726b580f522ef4585ed6411d20f6fa6a74dee

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

define Package/nethogs
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Linux 'net top' tool
	URL:=https://github.com/raboof/nethogs
	DEPENDS:=+libncursesw +libpcap +libstdcpp
endef

define Package/nethogs/description
 NetHogs is a small 'net top' tool. Instead of breaking the traffic
 down per protocol or per subnet, like most tools do, it groups bandwidth by
 process.
endef

MESON_ARGS += \
	-Denable-libnethogs=disabled

define Build/Prepare
	$(Build/Prepare/Default)
	$(SED) 's,@VERSION@,$(PKG_VERSION),' $(PKG_BUILD_DIR)/meson.build
endef

define Package/nethogs/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nethogs $(1)/opt/sbin
endef

$(eval $(call BuildPackage,nethogs))
