# PDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=exiv2
PKG_VERSION:=0.28.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/Exiv2/exiv2
PKG_MIRROR_HASH:=722cf8f5695edf2789ef037b49c70ba8c93c748bc445200a670e28a449821525

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING LICENSE.txt

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

define Package/exiv2/Default
	TITLE:=Image metadata library and tools
	URL:=https://exiv2.org/
endef

define Package/libexiv2
	$(call Package/exiv2/Default)
	SECTION:=libs
	CATEGORY:=Libraries
	DEPENDS:=+libcurl +libexpat +libinireader +libstdcpp +zlib
	TITLE+= (library)
endef

define Package/exiv2
	$(call Package/exiv2/Default)
	SECTION:=multimedia
	CATEGORY:=Multimedia
	DEPENDS:=+libexiv2
endef

define Package/libexiv2/description
 library and a command-line utility to read, write, delete and modify Exif,
 IPTC, XMP and ICC image metadata.
endef

Package/exiv2/description = $(Package/libexiv2/description)

MESON_ARGS += \
	-Dbrotli=disabled \
	-DunitTests=disabled

define Package/libexiv2/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libexiv2.so* $(1)/opt/lib
endef

define Package/exiv2/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/exiv2 $(1)/opt/bin
endef

$(eval $(call BuildPackage,libexiv2))
$(eval $(call BuildPackage,exiv2))
