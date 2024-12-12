# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=ltrace
PKG_REAL_VERSION:=0.7.91
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2023-07-05
PKG_SOURCE_VERSION:=8eabf684ba6b11ae7a1a843aca3c0657c6329d73
PKG_SOURCE_URL:=https://gitlab.com/cespedes/ltrace
PKG_MIRROR_HASH:=afbd764a2474d3bee6f1a2ef2aa5bcda4b28d21e663f6a33ed65519ecac24db9

PKG_VERSION:=$(PKG_REAL_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

PKG_CONFIG_DEPENDS:= \
	CONFIG_LTRACE_ELFUTILS \
	CONFIG_LTRACE_LIBUNWIND

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/ltrace
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=debugging program
  URL:=https://ltrace.org/
  DEPENDS:=+libelf +libstdcpp +LTRACE_ELFUTILS:libdw +LTRACE_LIBUNWIND:libunwind
endef

define Package/ltrace/description
 ltrace intercepts and records dynamic library calls which are
 called by an executed process and the signals received by that process. It
 can also intercept and print the system calls executed by the program.
endef

define Package/ltrace/config
choice
	prompt "Use unwinding support"
	default LTRACE_ELFUTILS

	config LTRACE_ELFUTILS
		bool "elfutils (libdw)"
		help
			Use elfutils libdwfl unwinding support.

	config LTRACE_LIBUNWIND
		bool "libunwind"
		depends on !( mips||mipsel )
		help
			Use libunwind frame unwinding support.

endchoice
endef

CONFIGURE_ARGS += \
	--with$(if $(CONFIG_LTRACE_ELFUTILS),,out)-elfutils \
	--with$(if $(CONFIG_LTRACE_LIBUNWIND),,out)-libunwind

# or
#CONFIGURE_ARGS += \
#	--with-elfutils=$(if $(CONFIG_LTRACE_ELFUTILS),yes,no) \
#	--with-libunwind=$(if $(CONFIG_LTRACE_LIBUNWIND),yes,no)

CONFIGURE_VARS += \
	ac_cv_lib_selinux_security_get_boolean_active=no

define Package/ltrace/conffiles
/opt/share/ltrace
endef

define Package/ltrace/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/ltrace $(1)/opt/bin

	$(INSTALL_DIR) $(1)/opt/share/ltrace
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/share/ltrace/*.conf $(1)/opt/share/ltrace
endef

$(eval $(call BuildPackage,ltrace))
