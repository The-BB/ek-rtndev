# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=tty-solitaire
PKG_VERSION:=1.4.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/mpereira/tty-solitaire
PKG_MIRROR_HASH:=dc29290edc00632accb455c1b5a22ed8a9a4c1756df79fb752574d791d154ee7

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/tty-solitaire
  SECTION:=games
  CATEGORY:=Games
  TITLE:=klondike solitaire game
  URL:=https://github.com/mpereira/tty-solitaire
  DEPENDS:=+libncursesw
endef

define Package/tty-solitaire/description
 Ncurses-based klondike solitaire game.
endef

TARGET_CFLAGS += \
	-I$(STAGING_DIR)/opt/include/ncursesw

define Package/tty-solitaire/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ttysolitaire $(1)/opt/bin
endef

$(eval $(call BuildPackage,tty-solitaire))
