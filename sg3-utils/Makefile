# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2019-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=sg3-utils
PKG_VERSION:=1.48
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/hreinecke/sg3_utils
PKG_MIRROR_HASH:=76cc8b6a83a2be1e2fd071ea7dba8c8a249e240125c85618ca48cf7c08e730be

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=BSD-2-Clause GPL-2.0-or-later
PKG_LICENSE_FILES:=BSD_LICENSE COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/sg3-utils
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Disc
  TITLE:=utilities that send SCSI commands to devices
  URL:=https://sg.danny.cz/sg/sg3_utils.html
  PROVIDES:=sg3_utils
endef

define Package/sg3-utils/description
 This package contains utilities that send SCSI commands to devices.
 As well as devices on transports traditionally associated with SCSI (e.g. Fibre
 Channel (FCP), Serial Attached SCSI (SAS) and the SCSI Parallel Interface(SPI))
 many other devices use SCSI command sets. ATAPI cd/dvd drives and SATA disks that
 connect via a translation layer or a bridge device are examples of devices that
 use SCSI command sets.
endef

define Package/sg3-utils/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/bin $(1)/opt
	$(SED) 's|/bin/bash|/bin/sh|g' \
		$(1)/opt/bin/rescan-scsi-bus.sh
	$(SED) 's|/bin/bash|/bin/sh|g' \
		$(1)/opt/bin/scsi_{logging_level,mandat,readcap,ready,satl,start,stop,temperature}
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/lib*.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,sg3-utils))
