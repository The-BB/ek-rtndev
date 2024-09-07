# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2019-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=nmon
PKG_VERSION:=16q
PKG_RELEASE:=1

PKG_SOURCE:=lmon$(PKG_VERSION).c
PKG_SOURCE_URL:=@SF/nmon
PKG_HASH:=1b78a81672c19291b3d11a6e319dd9b23a022a262dba1efcea008d6df51aca51

PKG_MAINTAINER:=Thomas Kupper <thomas.kupper@gmail.com>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE-GPL2

UNPACK_CMD=$(CP) $(DL_DIR)/$(PKG_SOURCE) $(1)

include $(INCLUDE_DIR)/package.mk

define Package/nmon
	SECTION:=nmon
	CATEGORY:=Administration
	TITLE:=Nigel's performance Monitor for Linux
	URL:=https://nmon.sourceforge.io/pmwiki.php
	DEPENDS:=+libncursesw
endef

define Package/nmon/description
 Linux performance monitoring on-screen or to CSV file.
endef

TARGET_CFLAGS += -DGETUSER -DJFS -DKERNEL_2_6_18 -DLARGEMEM
TARGET_LDFLAGS += -lncursesw -lm

define Build/Compile
	$(TARGET_CC) $(PKG_BUILD_DIR)/$(MAKE_PATH)/$(PKG_SOURCE) -o $(PKG_BUILD_DIR)/$(PKG_NAME) \
		$(TARGET_CFLAGS) $(TARGET_LDFLAGS)
endef

define Package/nmon/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/opt/bin
endef

$(eval $(call BuildPackage,nmon))
