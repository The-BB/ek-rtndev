#
# Copyright (C) 2019-2021 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# 1.45 and 1.46 suffers from following error, whenever HAVE_NVME enabled or disabled^
# sg_pt_linux_nvme.c:1913:9: error: 'vb' undeclared

include $(TOPDIR)/rules.mk

PKG_NAME:=sg3_utils
PKG_VERSION:=1.44
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=ed2e1216453184d7888122a32a6c1e58ebc6a2c6
PKG_SOURCE_URL:=https://github.com/hreinecke/sg3_utils
PKG_MIRROR_HASH:=f92cad04d7b1ac41eda298819e9b6b4f08398474a6e2ed7d985c88232ea6fe90

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/sg3_utils
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Disc
	TITLE:=utilities that send SCSI commands to devices
	URL:=http://sg.danny.cz/sg/sg3_utils.html
	MAINTAINER:=Entware team, https://entware.net
endef

define Package/sg3_utils/description
 This package contains utilities that send SCSI commands to devices. As well as
 devices on transports traditionally associated with SCSI (e.g. Fibre Channel
 (FCP), Serial Attached SCSI (SAS) and the SCSI Parallel Interface(SPI)) many
 other devices use SCSI command sets. ATAPI cd/dvd drives and SATA disks that
 connect via a translation layer or a bridge device are examples of devices
 that use SCSI command sets.
endef

define Package/sg3_utils/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/bin $(1)/opt
	$(SED) 's|/bin/bash|/bin/sh|g' \
		$(1)/opt/bin/rescan-scsi-bus.sh
	$(SED) 's|/bin/bash|/bin/sh|g' \
		$(1)/opt/bin/scsi_{logging_level,mandat,readcap,ready,satl,start,stop,temperature}
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/lib*.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,sg3_utils))
