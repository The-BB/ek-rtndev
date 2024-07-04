#
# Copyright (C) 2011-2023 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tsmuxer
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2023-05-26
PKG_SOURCE_VERSION:=ddadf58f0c139d95451a5dac836f79dfd17e143d
PKG_SOURCE_URL:=https://github.com/justdan96/tsMuxer.git
PKG_MIRROR_HASH:=56ed90517dfe66bbd0f448ee24fb38c0db1cd9045e77861162f4d928e8432bf4

PKG_VERSION=2.6.16_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/tsmuxer
	SECTION:=multimedia
	CATEGORY:=Multimedia
	DEPENDS:=+libfreetype +libstdcpp
	TITLE:=transport stream (re)muxer
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/tsmuxer/description
 tsMuxer is a transport stream muxer for remuxing/muxing elementary streams,
 EVO/VOB/MPG, MKV/MKA, MP4/MOV, TS, M2TS to TS to M2TS. Supported video codecs
 H.264/AVC, H.265/HEVC, VC-1, MPEG2. Supported audio codecs AAC, (E-)AC3(DD+),
 DTS/ DTS-HD.
endef

define Package/tsmuxer/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/tsmuxer $(1)/opt/bin
endef

$(eval $(call BuildPackage,tsmuxer))
