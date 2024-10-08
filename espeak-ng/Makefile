# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# 1.51 and 1.51.1 fails to compile: unknown type name 'espeak_ng_OUTPUT_HOOKS'

include $(TOPDIR)/rules.mk

PKG_NAME:=espeak-ng
PKG_VERSION:=1.50
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=b702b03996de94035fadae0eb5ad9506c5a09f35
PKG_SOURCE_URL:=https://github.com/espeak-ng/espeak-ng.git
PKG_MIRROR_HASH:=13c25bb0ad5863500535586c2f8702c1bcc46b2879095a8a8e448e6be6be0d27

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_DEPENDS:=espeak-ng/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/espeak-ng/Default
	TITLE:=speech synthesizer
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
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
	DEPENDS:=+libespeak-ng
endef

define Package/libespeak-ng/description
 eSpeak NG is an open source speech synthesizer that supports more than
 hundred languages and accents.
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

define Host/Prepare
	$(LN) $(HOST_BUILD_DIR)/README.md $(HOST_BUILD_DIR)/README
	$(call Host/Prepare/Default)
endef

CONFIGURE_ARGS += \
	--with-extdict-ru \
	--with-extdict-zh \
	--with-extdict-zhy

CONFIGURE_VARS += \
	HOST_BUILD_DIR="$(HOST_BUILD_DIR)"

define Build/Prepare
	$(LN) $(PKG_BUILD_DIR)/README.md $(PKG_BUILD_DIR)/README
	$(call Build/Prepare/Default)
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
