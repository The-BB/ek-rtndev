# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2020-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=isync
PKG_VERSION:=1.5.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)/$(PKG_VERSION)
PKG_HASH:=a0c81e109387bf279da161453103399e77946afecf5c51f9413c5e773557f78d

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:= \
	COPYING \
	LICENSES/GPL-2.0-or-later.txt \
	LICENSES/LicenseRef-isync-GPL-exception.txt

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/isync
	SECTION:=mail
	CATEGORY:=Mail
	TITLE:=mailbox synchronization program
	URL:=https://isync.sourceforge.io/
	DEPENDS:=+libdb47 +libsasl2 +openssl-util
endef

define Package/isync/description
 isync is a command line application which synchronizes mailboxes;
 currently Maildir and IMAP4 mailboxes are supported. New messages, message
 deletions and flag changes can be propagated both ways. isync is suitable
 for use in IMAP-disconnected mode.
endef

define Package/isync/install
	$(INSTALL_DIR) $(1)/opt
	$(CP) $(PKG_INSTALL_DIR)/opt/bin $(1)/opt
endef

$(eval $(call BuildPackage,isync))
