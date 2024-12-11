# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=espeak-ng
PKG_VERSION:=1.51.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/espeak-ng/espeak-ng
PKG_MIRROR_HASH:=986dbf4a9030512cc28affb5b08687d80f3f33342fc38fdb90d1335c15058724

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING COPYING.APACHE COPYING.BSD2 COPYING.UCD

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

PKG_BUILD_DEPENDS:=espeak-ng/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

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

HOST_CONFIGURE_ARGS += \
	--disable-shared \
	--without-gradle \
	--without-pcaudiolib \
	--without-klatt \
	--without-mbrola \
	--without-sonic

HOST_CONFIGURE_VARS += \
	HOST_BUILD_DIR="$(HOST_BUILD_DIR)"

CONFIGURE_VARS += \
	HOST_BUILD_DIR="$(HOST_BUILD_DIR)"

define Host/Prepare
	$(call Host/Prepare/Default)
	( cd $(HOST_BUILD_DIR); \
		touch AUTHORS; \
		$(LN) CHANGELOG.md NEWS; \
		$(LN) README.md README; \
	)
endef

Host/Install:=:

define Build/Prepare
	$(call Build/Prepare/Default)
	( cd $(PKG_BUILD_DIR); \
		touch AUTHORS; \
		$(LN) CHANGELOG.md NEWS; \
		$(LN) README.md README; \
	)
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
