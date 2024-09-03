# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# Abandoned in 2020

include $(TOPDIR)/rules.mk

PKG_NAME:=vblade
PKG_VERSION:=25
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/OpenAoE/vblade
PKG_MIRROR_HASH:=8e6558ee06073a1f5c82274f34a10d321b044ef9b690703af5ab97170066d350

include $(INCLUDE_DIR)/package.mk

define Package/vblade
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Filesystem
	TITLE:=AoE storage target
	URL:=$(PKG_SOURCE_URL)
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/vblade/description
 The vblade is a minimal ATA over Ethernet (AoE) storage target. Its
 focus is simplicity, not performance or richness of features. It
 exports a seekable file available over an ethernet local area network
 (LAN) via the AoE data storage protocol.
endef

define Package/vblade/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/vblade $(1)/opt/bin
endef

$(eval $(call BuildPackage,vblade))
