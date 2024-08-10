# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# The newer versions requires CUDA libraries

include $(TOPDIR)/rules.mk

PKG_NAME:=task-spooler
PKG_VERSION:=1.3.0
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=052db94bc588e4f4471e37599dfdff77dc44c8bb
PKG_SOURCE_URL:=https://github.com/justanhduc/task-spooler.git
PKG_MIRROR_HASH:=d876964402559d1d4d68ec86159a86d94bdb947b008357fe491718353ff979a7

include $(INCLUDE_DIR)/package.mk

define Package/task-spooler
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=task spooler
	URL:=http://tcforge.berlios.de/
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/task-spooler/description
 Task spooler is a Unix batch system where the tasks spooled run one after
 the other. The amount of jobs to run at once can be set at any time. Each user
 in each system has his own job queue. The tasks are run in the correct context
 (that of enqueue) from any shell/process, and itask-spooler output/resultask-spooler can be easily
 watched.
endef

define Package/task-spooler/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ts $(1)/opt/bin/tsp
endef

$(eval $(call BuildPackage,task-spooler))
