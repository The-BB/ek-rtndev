# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2025 Entware

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=pnpm
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=9.15.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NPM_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=https://registry.npmjs.org/$(PKG_NPM_NAME)/-/
PKG_HASH:=9bee59c7313a216722c079c1e22160dea7f88df4e0c3450b1d7b01b882336c6a

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

HOST_BUILD_DEPENDS:=node/host
HOST_BUILD_PARALLEL:=1

PKG_HOST_ONLY:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/node-pnpm
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Fast, disk space efficient package manager
  URL:=https://pnpm.io/
  DEPENDS:=+node
  BUILDONLY:=1
endef

define Package/node-pnpm/description
  Fast, reliable, and secure dependency management.
endef

TAR_OPTIONS+= --strip-components 1
TAR_CMD=$(HOST_TAR) -C $(1) $(TAR_OPTIONS)

HOSTTMPNPM:=$(shell mktemp -u XXXXXXXXXX)

HOST_NPM_FLAGS=$(HOST_MAKE_VARS) \
	$(HOST_MAKE_FLAGS) \
	npm_config_arch=$(NODEJS_CPU) \
	npm_config_target_arch=$(NODEJS_CPU) \
	npm_config_build_from_source=true \
	npm_config_nodedir=$(STAGING_DIR)/opt/ \
	npm_config_prefix=$(HOST_INSTALL_DIR)/usr/ \
	npm_config_cache=$(TMP_DIR)/npm-cache-$(HOSTTMPNPM) \
	npm_config_tmp=$(TMP_DIR)/npm-tmp-$(HOSTTMPNPM)

define Host/Compile
	$(HOST_NPM_FLAGS) npm i -g --production $(HOST_BUILD_DIR)
	$(HOST_NPM_FLAGS) npm i \
		--production \
		--prefix=$(HOST_BUILD_DIR) \
		--target_arch=$(NODEJS_CPU) \
		--prefer-dedupe
	rm -rf $(TMP_DIR)/npm-tmp-$(HOSTTMPNPM)
	rm -rf $(TMP_DIR)/npm-cache-$(HOSTTMPNPM)
endef

define Host/Install
	$(INSTALL_DIR) $(1)/lib/node_modules/$(PKG_NPM_NAME)
	$(CP) $(HOST_INSTALL_DIR)/usr/lib/node_modules/$(PKG_NPM_NAME)/{package.json,LICENSE} \
		$(1)/lib/node_modules/$(PKG_NPM_NAME)/
	$(CP) $(HOST_INSTALL_DIR)/usr/lib/node_modules/$(PKG_NPM_NAME)/README.md \
		$(1)/lib/node_modules/$(PKG_NPM_NAME)/
	$(CP) $(HOST_INSTALL_DIR)/usr/lib/node_modules/$(PKG_NPM_NAME)/{bin,dist} \
		$(1)/lib/node_modules/$(PKG_NPM_NAME)/
	$(INSTALL_DIR) $(1)/bin
	$(LN) ../lib/node_modules/$(PKG_NPM_NAME)/bin/pnpm.cjs $(1)/bin/pnpm
	$(LN) ../lib/node_modules/$(PKG_NPM_NAME)/bin/pnpx.cjs $(1)/bin/pnpx
endef

define Host/Clean
	rm -f $(STAGING_DIR_HOSTPKG)/bin/pnp{m,x}
	rm -rf $(STAGING_DIR_HOSTPKG)/lib/node_modules/pnpm
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,node-pnpm))
