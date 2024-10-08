# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2021 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=rtmpdump
PKG_VERSION:=2.4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2021-02-19
PKG_SOURCE_VERSION:=f1b83c10d8beb43fcc70a6e88cf4325499f25857
PKG_SOURCE_URL:=https://git.ffmpeg.org/rtmpdump.git
PKG_MIRROR_HASH:=18d001a03861b4d80300ab5a68484e2bca67bd84a0e58749418a5e87553e316d

PKG_VERSION:=$(PKG_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/rtmpdump/Default
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libgnutls +zlib
	TITLE:=a toolkit for RTMP streams
	URL:=https://rtmpdump.mplayerhq.hu/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/librtmp
	$(call Package/rtmpdump/Default)
endef

define Package/rtmpdump
	$(call Package/rtmpdump/Default)
	DEPENDS:=+librtmp
endef

define Package/librtmp/description
 librtmp is a RTMPDump Real-Time Messaging Protocol API.
endef

define Package/rtmpdump/description
 rtmpdump is a toolkit for RTMP streams. All forms of RTMP are supported.
endef

MAKE_VARS += \
	XCFLAGS="$(TARGET_CFLAGS) -I$(STAGING_DIR)/opt/include" \
	XLDFLAGS="$(TARGET_LDFLAGS)"

MAKE_FLAGS += \
	prefix="/opt"

define Package/librtmp/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/librtmp.so.1 $(1)/opt/lib
endef

define Package/rtmpdump/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/rtmpdump $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/rtmp{gw,srv,suck} $(1)/opt/sbin
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/librtmp.* $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/librtmp.pc $(1)/opt/lib/pkgconfig
	$(INSTALL_DIR) $(1)/opt/include/librtmp
	$(CP) $(PKG_INSTALL_DIR)/opt/include/librtmp/*.h $(1)/opt/include/librtmp
endef

$(eval $(call BuildPackage,librtmp))
$(eval $(call BuildPackage,rtmpdump))
