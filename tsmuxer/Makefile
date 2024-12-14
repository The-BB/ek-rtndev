# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=tsmuxer
PKG_REAL_VERSION:=2.6.16
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2024-06-06
PKG_SOURCE_VERSION:=7f8667d1e6100a5b6407340d91ad80d57d976e58
PKG_SOURCE_URL:=https://github.com/justdan96/tsMuxer
PKG_MIRROR_HASH:=46440bbff2d903ec989273f963d9a92a67265dc3715d04f1f57508873b784d56

PKG_VERSION:=$(PKG_REAL_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/tsmuxer
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=transport stream (re)muxer
	URL:=$(PKG_SOURCE_URL)
	DEPENDS:=+libfreetype +libstdcpp
endef

define Package/tsmuxer/description
 tsMuxer is a transport stream muxer for remuxing/muxing elementary
 streams, EVO/VOB/MPG, MKV/MKA, MP4/MOV, TS, M2TS to TS to M2TS.
 Supported video codecs H.264/AVC, H.265/HEVC, VC-1, MPEG2.
 Supported audio codecs AAC, (E-)AC3(DD+), DTS/ DTS-HD.
endef

define Package/tsmuxer/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/tsmuxer $(1)/opt/bin
endef

$(eval $(call BuildPackage,tsmuxer))
