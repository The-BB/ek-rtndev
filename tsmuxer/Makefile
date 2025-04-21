# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

# Project archieved

include $(TOPDIR)/rules.mk

PKG_NAME:=tsmuxer
PKG_VERSION:=2.7.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/justdan96/tsMuxer
PKG_MIRROR_HASH:=14c991a85ff374d81c6573188e694e6ccf9920ad7125bb9ee667bd03ffd3d28b

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/tsmuxer
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=transport stream (re)muxer
  URL:=https://justdan96.github.io/tsMuxer/
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
