# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=locales
PKG_VERSION:=$(LIBC_VERSION)
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/locales
	SECTION:=libs
	CATEGORY:=Base system
	DEPENDS:=+grep @USE_GLIBC
	TITLE:=locales support (independent of system lib)
	URL:=http://gcc.gnu.org/
	MAINTAINER:=Entware team, https://entware.net
endef

LVERSION1:=$(call qstrip,$(CONFIG_GLIBC_VERSION))
LVERSION2:=$(subst .,,$(LVERSION1))

ilocales=de_DE en_US en_GB fr_FR it_IT ru_RU i18n \
	$(if $(or $(CONFIG_GLIBC_USE_VERSION_2_27), \
		$(CONFIG_GLIBC_USE_VERSION_2_33), \
		$(CONFIG_GLIBC_USE_VERSION_2_34)),i18n_ctype) \
	iso14651_t1 iso14651_t1_common \
	translit_circle translit_combining translit_font translit_narrow translit_small \
	translit_cjk_compat translit_compat translit_fraction translit_neutral translit_wide

icharmaps=ANSI_X3.4-1968.gz UTF-8.gz

define Build/Configure
endef

define Build/Compile
endef

define Package/locales/install
	$(INSTALL_DIR) $(1)/opt/lib/locale
	$(INSTALL_DIR) $(1)/opt/share/i18n/locales
	$(INSTALL_DIR) $(1)/opt/share/i18n/charmaps
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(TOOLCHAIN_DIR)/bin/locale $(1)/opt/bin/locale.new
	$(CP) $(TOOLCHAIN_DIR)/bin/localedef $(1)/opt/bin/localedef.new
	for file in $(ilocales); do \
		$(CP) $(TOOLCHAIN_DIR)/share/i18n/locales/$$$$file $(1)/opt/share/i18n/locales ; \
	done ; \
	for file in $(icharmaps); do \
		$(CP) $(TOOLCHAIN_DIR)/share/i18n/charmaps/$$$$file $(1)/opt/share/i18n/charmaps ; \
	done ; \
	exit 0
endef

define Package/locales/preinst
#!/bin/sh

if [ -x '/opt/bin/locale.new' ] && [ -z "$$(/opt/bin/locale.new -V | grep $(LVERSION1))" ]; then
	echo 'locale-archive needs upgrade, deleting old one.'
	rm -f /opt/lib/locale/locale-archive
fi
exit 0
endef

define Package/locales/postinst
#!/bin/sh

echo 'Entware uses separate locale-archive file independent from main system'
if ! [ -f '/opt/lib/locale/locale-archive' ]; then
	mkdir -p /opt/lib/locale
	echo 'Creating locale archive /opt/lib/locale/locale-archive'
	echo 'Adding en_EN.UTF-8'
	/opt/bin/localedef.new -c -f UTF-8 -i en_US en_US.UTF-8
	echo 'Adding ru_RU.UTF-8'
	/opt/bin/localedef.new -c -f UTF-8 -i ru_RU ru_RU.UTF-8
fi
if ! [ -f '/opt/lib/locale/locale-archive' ]; then
	echo 'locale-archive file was not created, not enough memory? Downloading...'
	wget http://bin.entware.net/other/locale-archive.$(LVERSION1)$(if $(CONFIG_BIG_ENDIAN),.be,) -O /opt/lib/locale/locale-archive
fi
echo 'You can download locale sources from http://bin.entware.net/other/i18n_glib$(LVERSION2).tar.gz'
echo 'You can add new locales to Entware using /opt/bin/localedef.new'
exit 0
endef

$(eval $(call BuildPackage,locales))
