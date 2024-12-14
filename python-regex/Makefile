# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=python-regex
PKG_VERSION:=2024.11.6
PKG_RELEASE:=1

PYPI_NAME:=regex
PKG_HASH:=7ab159b063c52a0333c884e4679f8d7a85112ee3078fe3d9004b2dd875585519

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE.txt

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-regex
	SECTION:=lang
	CATEGORY:=Languages
	SUBMENU:=Python
	TITLE:=alternative regular expression module, to replace re
	URL:=https://github.com/mrabarnett/mrab-regex
	DEPENDS:=+python3-codecs +python3-urllib
endef

define Package/python3-regex/description
 This regex implementation is backwards-compatible with the standard
 're' module, but offers additional functionality.
endef

define Package/python3-regex/postrm
#!/bin/sh

rm -rf $(PYTHON3_PKG_DIR)/$(PYPI_NAME)
rm -rf $(PYTHON3_PKG_DIR)/$(PYPI_NAME)-$(PKG_VERSION).dist-info
endef

$(eval $(call Py3Package,python3-regex))
$(eval $(call BuildPackage,python3-regex))
