#
# Copyright (C) 2020-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=freediameter
PKG_VERSION:=1.5.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=8ac823b77653a03da82232470b376c2b281b0973
PKG_SOURCE_URL:=https://github.com/freeDiameter/freeDiameter
PKG_MIRROR_HASH:=5cac14aff0dd632402b14b286ccfa875a7d56accd3741171bb4b8519b97b60c8

# FIXME ninja: error: manifest 'build.ninja' still dirty after 100 tries
PKG_USE_NINJA:=0
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/freediameter
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libgcrypt +libgnutls +libidn
	TITLE:=Diameter proto implementation
	URL:=http://www.freediameter.net
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/freediameter/description
 freeDiameter provides an extensible platform for deploying a Diameter network
 for your Authentication, Authorization and Accounting needs, whether you are
 involved in research or a network operator.
endef

CMAKE_OPTIONS += \
	-DDISABLE_SCTP=YES

define Build/InstallDev
	true
endef

define Package/freediameter/install
	$(INSTALL_DIR) $(1)/opt
	$(CP) $(PKG_INSTALL_DIR)/opt/{bin,lib} $(1)/opt
endef

$(eval $(call BuildPackage,freediameter))
