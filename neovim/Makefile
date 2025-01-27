# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2023-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=neovim
PKG_VERSION:=0.10.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/neovim/neovim/tar.gz/refs/tags/v$(PKG_VERSION)?
PKG_HASH:=39fab47d241da7b9418823cc563c689d522c1c4b2def04036393834f3f1ca94c

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE.txt

PKG_BUILD_DEPENDS:=lua/host lua-ffi/host luabitop/host
PKG_BUILD_DEPENDS+=liblpeg libtermkey libvterm tree-sitter unibilium

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/neovim
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Editors
  TITLE:=hyperextensible Vim-based text editor
  URL:=https://neovim.io
  PKG_MAINTAINER:=Entware team, https://entware.net
  DEPENDS:=+libncursesw +libuv +luajit +luv +msgpack-c @HAS_LUAJIT_ARCH $(INTL_DEPENDS)
endef

define Package/neovim/description
  Vim-fork focused on extensibility and usability.
endef

CMAKE_BINARY_SUBDIR:=build-cross

TARGET_CFLAGS += -pthread
TARGET_LDFLAGS += -lncursesw

define Build/Compile
	( cd $(PKG_BUILD_DIR); $(INSTALL_DIR) .deps-cross; \
		CC=$(TARGET_CC) CFLAGS="$(TARGET_CFLAGS)" \
		$(MAKE) -C .deps-cross \
		BUNDLED_CMAKE_FLAG="\
			-DCMAKE_BUILD_TYPE=Release \
			-DUSE_BUNDLED=OFF \
			-DUSE_BUNDLED_LUV=ON \
			-DUSE_BUNDLED_TS=ON \
			-DUSE_BUNDLED_LIBVTERM=ON \
			-DUSE_BUNDLED_LIBUV=ON \
			-DUSE_BUNDLED_LUAJIT=OFF \
			-DUSE_BUNDLED_LUA=ON \
			-DUSE_BUNDLED_LPEG=ON \
			-DUSE_BUNDLED_MSGPACK=ON \
			-DUSE_BUNDLED_UNIBILIUM=ON \
			-DUSE_BUNDLED_TS_PARSERS=ON \
			-DLUA_INCLUDE_DIR=$(STAGING_DIR)/opt/include \
			-DLUA_LIBRARY=$(STAGING_DIR)/opt/lib/liblua.a" \
		-f ../Makefile deps; \
	)
	( cd $(PKG_BUILD_DIR); \
		cmake -S cmake.deps -B .deps -G "Ninja" -DCMAKE_BUILD_TYPE=Release; \
		cmake --build .deps -j$(NPROC); \
	)
	( cd $(PKG_BUILD_DIR); \
		cmake -B build-native -G "Ninja" -DCMAKE_BUILD_TYPE=Release; \
		cmake --build build-native -j$(NPROC); \
		$(CP) $(PKG_BUILD_DIR)/build-native/lib/libnlua0.so \
			$(STAGING_DIR_HOSTPKG)/lib/lua/5.1/nlua0.so; \
	)
endef

define Package/neovim/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nvim $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib/nvim/parser
	$(CP) \
		$(PKG_BUILD_DIR)/.deps-cross/.deps/usr/lib/nvim/parser/*.so \
			$(1)/opt/lib/nvim/parser
	$(INSTALL_DIR) $(1)/opt/share/nvim
	$(CP) $(PKG_INSTALL_DIR)/opt/share/nvim/runtime $(1)/opt/share/nvim
endef

$(eval $(call BuildPackage,neovim))
