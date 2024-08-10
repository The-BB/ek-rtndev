# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2024 Entware

# Abandoned in 2016

include $(TOPDIR)/rules.mk

PKG_NAME:=ltrace
PKG_VERSION:=0.7.9
PKG_RELEASE:=3

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=82c66409c7a93ca6ad2e4563ef030dfb7e6df4d4
PKG_SOURCE_URL:=https://github.com/dkogan/ltrace.git
PKG_MIRROR_HASH:=4927e88d902a8ef22955411c5bb8f03fe8e71a5222460e8160e23c22612fc00d

PKG_LICENSE:=GPL-2.0-only

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
  TITLE:=tracks runtime library calls in dynamically linked programs
  URL:=https://ltrace.org/
  DEPENDS:=+libelf +libstdcpp +LTRACE_ELFUTILS:libdw +LTRACE_LIBUNWIND:libunwind
endef

define Package/ltrace/description
 ltrace intercepts and records dynamic library calls which are called
by an executed process and the signals received by that process. It 
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
