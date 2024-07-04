#
# Copyright (C) 2011-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=vorbis-tools
PKG_VERSION:=1.4.2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=71687237c07cd9d5564c73990d0de45520c5bec1
PKG_SOURCE_URL:=https://github.com/xiph/vorbis-tools.git
PKG_MIRROR_HASH:=db0e7186d7f717b482d93c98040a8670fd90f405b968999844944aac140474f6

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/vorbis-tools
	SECTION:=sound
	CATEGORY:=Sound
	DEPENDS:=+libogg +libvorbis +libflac
	TITLE:=vorbis-tools and nothing else
	URL:=http://xiph.org/vorbis/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/vorbis-tools/description
 oggdec, oggenc, ogginfo, vcut, vorbiscomment command line utilities.
endef

CONFIGURE_ARGS += \
	--disable-ogg123 \
	--disable-oggtest \
	--disable-vorbistest \
	--disable-curltest

define Package/vorbis-tools/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
endef

$(eval $(call BuildPackage,vorbis-tools))
