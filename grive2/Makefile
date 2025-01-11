# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2021 Entware

# XXX boost bumped

include $(TOPDIR)/rules.mk

PKG_NAME:=grive2
PKG_VERSION:=0.5.3
PKG_RELEASE:=6

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=d03c4a24ceb179d0fdb4c47e3d144d547ffcc8b6
PKG_SOURCE_URL:=https://github.com/vitalif/grive2
PKG_MIRROR_HASH:=20eaafe0cb4fe0c58ef6ba0bbfd8f7be9f3b4f5de32cdc3d67edbdf43f00d43c

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
include $(INCLUDE_DIR)/nls.mk

define Package/grive2
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Filesystem
	DEPENDS:=+libcurl +yajl +libstdcpp +libgcrypt +libbfd +boost-filesystem \
		+boost-program_options +boost-regex +boost-test +boost-system
	TITLE:=a fork of original Google Drive client
	URL:=https://github.com/vitalif/grive2
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/grive2/description
 This is the fork of original "Grive" (https://github.com/Grive/grive) Google
 Drive client with the support for the new Drive REST API and partial sync.
endef

TARGET_CXXFLAGS += -fpermissive -DBOOST_BIND_GLOBAL_PLACEHOLDERS
TARGET_LDFLAGS += $(if $(INTL_FULL),-lintl)

ifneq ($(CONFIG_USE_GLIBC),y)
define Build/Prepare
	$(Build/Prepare/Default)
	$(SED) 's,find_package(BFD),#find_package(BFD),g' $(PKG_BUILD_DIR)/libgrive/CMakeLists.txt
endef
endif

define Package/grive2/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/grive $(1)/opt/bin
endef

$(eval $(call BuildPackage,grive2))
