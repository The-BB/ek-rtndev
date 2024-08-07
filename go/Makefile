# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=go
PKG_VERSION:=1.22.5
PKG_RELEASE:=1

PKG_SOURCE:=go$(PKG_VERSION).src.tar.gz
PKG_SOURCE_URL:=https://dl.google.com/go
PKG_HASH:=ac9c723f224969aee624bc34fd34c9e13f2a212d75c71c807de644bb46e112f6

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/golang/go_env.mk

PKG_UNPACK:=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xf $(DL_DIR)/$(PKG_SOURCE)

define Package/go/Default
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=The Go Programming Language
	URL:=https://golang.org/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/go
	$(call Package/go/Default)
	VARIANT:=hf
endef

define Package/go_nohf
	$(call Package/go/Default)
	VARIANT:=nohf
	DEPENDS:=@arm
endef

define Package/go/description
 Go is an open source programming language that makes it
 easy to build simple, reliable, and efficient software.
endef

Package/go_nohf/description=$(Package/go/description)

BINTYPE:=$(shell uname -m | sed 's/aarch64/arm64/;s/i[3-6]86/386/;s/x86_64/amd64/')

RSTRIP:=:
STRIP:=:

Build/Configure:=:

define Build/Compile
	( \
		cd $(PKG_BUILD_DIR)/src; \
		$(GO_VARS) GO_LDFLAGS="-s -w" PKG_CONFIG=/opt/bin/pkg-config \
		GOROOT_BOOTSTRAP=$(STAGING_DIR_HOST)/go ./make.bash --no-banner; \
	)
	if [ -d "$(PKG_BUILD_DIR)/bin/linux_$(GOARCH)" ]; then \
		rm $(PKG_BUILD_DIR)/bin/go{,fmt}; \
		mv $(PKG_BUILD_DIR)/bin/linux_$(GOARCH)/* $(PKG_BUILD_DIR)/bin/; \
		rm -rf $(PKG_BUILD_DIR)/{bin,pkg}/linux_$(GOARCH); \
	fi
	[ "$(BINTYPE)" = "$(GOARCH)" ] || rm -rf $(PKG_BUILD_DIR)/pkg/linux_$(BINTYPE)
	[ "$(BINTYPE)" = "$(GOARCH)" ] || rm -rf $(PKG_BUILD_DIR)/pkg/tool/linux_$(BINTYPE)
endef

define Package/go/install
	$(INSTALL_DIR) $(1)/opt/bin/go
	$(CP) $(PKG_BUILD_DIR)/{api,bin,lib,misc,pkg,test,doc,src} $(1)/opt/bin/go
	# Entware specific: fix exec path in scripts
	$(FIND) $(1)/opt/bin/go -type f | $(XARGS) $(SED) \
		's,^#!.*bash,#!/opt/bin/bash,;s,^#!.*perl,#!/opt/bin/perl,'
endef

Package/go_nohf/install=$(Package/go/install)

define Package/go/postinst
#!/bin/sh

echo "Please add /opt/bin/go/bin to your PATH"
endef

Package/go_nohf/postinst=$(Package/go/postinst)

$(eval $(call BuildPackage,go))
$(eval $(call BuildPackage,go_nohf))
