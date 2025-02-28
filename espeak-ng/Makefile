# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=espeak-ng
PKG_VERSION:=1.52.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/espeak-ng/espeak-ng
PKG_MIRROR_HASH:=9d5b1baeb92b0f76e31083533ff3d702e3508c48f0867d72436dd8670c0ad123

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING COPYING.APACHE COPYING.BSD2 COPYING.UCD

HOST_PATCH_DIR:=

PKG_INSTALL:=1

PKG_BUILD_DEPENDS:=espeak-ng/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/espeak-ng/Default
	TITLE:=a multi-lingual software speech synthesizer
	URL:=https://github.com/espeak-ng/espeak-ng
	DEPENDS:=+libstdcpp
endef

define Package/libespeak-ng
	$(call Package/espeak-ng/Default)
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE+= (library)
endef

define Package/espeak-ng
	$(call Package/espeak-ng/Default)
	SECTION:=multimedia
	CATEGORY:=Multimedia
	DEPENDS+=+libespeak-ng
endef

define Package/libespeak-ng/description
 eSpeak NG is an open source speech synthesizer that supports more
 than hundred languages and accents.
endef

Package/espeak-ng/description = $(Package/libespeak-ng/description)

CMAKE_HOST_OPTIONS += \
	-DUSE_KLATT=OFF \
	-DUSE_LIBPCAUDIO=OFF \
	-DUSE_LIBSONIC=OFF \
	-DUSE_MBROLA=OFF

CMAKE_OPTIONS += \
	-DBUILD_SHARED_LIBS=ON \
	-DUSE_KLATT=OFF \
	-DUSE_LIBPCAUDIO=OFF \
	-DUSE_LIBSONIC=OFF \
	-DUSE_MBROLA=OFF

TARGET_CXXFLAGS += -pthread

Host/Install:=:

define Build/Prepare
	$(call Build/Prepare/Default)
	$(SED) 's,@HOST_BUILD_DIR@,$(HOST_BUILD_DIR),' $(PKG_BUILD_DIR)/cmake/data.cmake
endef

define Package/libespeak-ng/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libespeak-ng.so* $(1)/opt/lib
endef

define Package/espeak-ng/install
	$(INSTALL_DIR) $(1)/opt
	$(CP) $(PKG_INSTALL_DIR)/opt/bin $(1)/opt
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/espeak-ng-data $(1)/opt/share
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,libespeak-ng))
$(eval $(call BuildPackage,espeak-ng))
