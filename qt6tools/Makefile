# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2023-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=qttools
PKG_VERSION:=6.9.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/qt/qttools
PKG_MIRROR_HASH:=98899051614bfd510d2d98aa926113a3f65f3dc44bf28fe948449b53f140b3b9

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:= \
	BSD-3-Clause BSD-3-Clause BSL-1.0 \
	GPL-2.0-only GPL-3.0-only LGPL-3.0-only

PKG_LICENSE_FILES:= \
	LICENSES/BSD-3-Clause.txt \
	LICENSES/BSL-1.0.txt \
	LICENSES/GPL-2.0-only.txt \
	LICENSES/GPL-3.0-only.txt \
	LICENSES/LGPL-3.0-only.txt \
	LICENSES/Qt-GPL-exception-1.0.txt

HOST_BUILD_DEPENDS:=qt6base/host
PKG_HOST_ONLY:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/qt6tools
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Qt6
  TITLE:=Qt tools
  URL:=https://www.qt.io
  DEPENDS:=+libstdcpp
  BUILDONLY:=1
endef

ifneq ($(CONFIG_CCACHE),)
HOSTCC=$(HOSTCC_NOCACHE)
HOSTCXX=$(HOSTCXX_NOCACHE)
endif

CMAKE_HOST_OPTIONS += \
	-DBUILD_SHARED_LIBS=OFF \
	-DCMAKE_INSTALL_PREFIX=../Qt6 \
	-DCMAKE_SKIP_RPATH=TRUE \
	-DCMAKE_SKIP_INSTALL_RPATH=ON \
	-DFEATURE_clang=OFF \
	-DFEATURE_clangcpp=OFF \
	-DFEATURE_linguist=ON \
	-DFEATURE_qtattributionsscanner=OFF \
	-DFEATURE_qtplugininfo=OFF \
	-DQt6_DIR="$(HOST_BUILD_DIR)/../Qt6"

$(eval $(call HostBuild))
$(eval $(call BuildPackage,qt6tools))
