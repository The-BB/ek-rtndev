# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=ctags
PKG_VERSION:=6.1.0
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=7ad90a853a5aee974c757217c87a3b468855c2b1
PKG_SOURCE_URL:=https://github.com/universal-ctags/ctags
PKG_MIRROR_HASH:=627e0b7b4d8f81d4a0f55a42b5e7f4905069c2968a1c1482de8c89d5b29662ce

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/ctags
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=$(ICONV_DEPENDS) +jansson +libyaml +libxml2 +libpcre2
	TITLE:=Universal Ctags
	URL:=https://ctags.io
	MAINTAINER:=Entware team, https://entware.net
	ALTERNATIVES:=200:/opt/bin/etags:/opt/bin/ctags
endef

define Package/ctags/description
 Universal Ctags generates an index (or tag) file of language objects found in
 source files for many popular programming languages. This index makes it easy
 for text editors and other tools to locate the indexed items. Universal Ctags
 improves on traditional ctags because of its multilanguage support, its ability
 for the user to define new languages searched by regular expressions, and its
 ability to generate emacs-style TAGS files.
endef

CONFIGURE_ARGS += \
	--disable-seccomp \
	--enable-debugging \
	--enable-dependency-tracking \
	--enable-etags \
	--enable-macro-patterns \
	--enable-tmpdir=/opt/tmp

CONFIGURE_VARS += \
	PYTHON=$(STAGING_DIR_HOSTPKG)/bin/python3

define Package/ctags/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/{c,read}tags $(1)/opt/bin
endef

$(eval $(call BuildPackage,ctags))
