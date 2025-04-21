# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=task-spooler
PKG_VERSION:=2.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/justanhduc/task-spooler
PKG_MIRROR_HASH:=e2ff80f9ee15d7d6fae9aa0d9c04e2124b1bdc25999b31301929b8a760004312

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/task-spooler
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=a scheduler for GPU/CPU tasks
  URL:=https://justanhduc.github.io/2021/02/03/Task-Spooler.html
endef

define Package/task-spooler/description
 Task spooler is a Unix batch system where the tasks spooled
 run one after the other. The amount of jobs to run at once can be set at
 any time. Each user in each system has his own job queue. The tasks are
 run in the correct context (that of enqueue) from any shell/process, and
 itask-spooler output/resultask-spooler can be easily watched.
endef

CMAKE_OPTIONS += \
	-DTASK_SPOOLER_COMPILE_CUDA=OFF

define Build/Configure
	$(call Build/Configure/Default)
	( cd $(PKG_BUILD_DIR); \
		$(HOSTCC) $(HOST_CFLAGS) -DTS_VERSION=$(PKG_VERSION) \
		man.c -o makeman; \
	)
endef

define Package/task-spooler/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/ts $(1)/opt/bin/tsp
endef

$(eval $(call BuildPackage,task-spooler))
