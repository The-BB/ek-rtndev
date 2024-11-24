# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2023-2024 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=qtbase
PKG_VERSION:=6.8.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/qt/qtbase
PKG_MIRROR_HASH:=52ec768c181896353af74bfac6ff8a777a17d3a765cc705ef981900cab3dcbff

PKG_LICENSE:= \
	GPL-2.0-or-later GPL-3.0-only GFDL-1.3-only LGPL-3.0-only \
	Apache-2.0 BSD-3-Clause BSL-1.0 MIT

PKG_LICENSE_FILES:= \
	LICENSES/Apache-2.0.txt \
	LICENSES/BSD-3-Clause.txt \
	LICENSES/BSL-1.0.txt \
	LICENSES/GFDL-1.3-no-invariants-only.txt \
	LICENSES/GPL-2.0-only.txt \
	LICENSES/GPL-3.0-only.txt \
	LICENSES/LGPL-3.0-only.txt \
	LICENSES/MIT.txt \
	LICENSES/Qt-GPL-exception-1.0.txt

PKG_BUILD_DEPENDS:=qt6base/host

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/qt6/Default
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=Qt6
  TITLE:=Qt6
  URL:=https://www.qt.io
  DEPENDS:=+libstdcpp
  BUILDONLY:=1
endef

define Package/qt6-core
  $(call Package/qt6/Default)
  TITLE+=Core module
  DEPENDS+=+libatomic +libopenssl $(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

define Package/qt6-network
  $(call Package/qt6/Default)
  TITLE+=Network module
  DEPENDS+=+qt6-core
endef

define Package/qt6-sql
  $(call Package/qt6/Default)
  TITLE+=Sql module
  DEPENDS+=+qt6-core
endef

define Package/qt6-xml
  $(call Package/qt6/Default)
  TITLE+=Xml module
  DEPENDS+=+qt6-core
endef

ifneq ($(CONFIG_CCACHE),)
HOSTCC=$(HOSTCC_NOCACHE)
HOSTCXX=$(HOSTCXX_NOCACHE)
endif

QT6_COMMON_OPTIONS:= \
	-DBUILD_SHARED_LIBS=OFF \
	\
	-DCMAKE_SKIP_RPATH=TRUE \
	-DCMAKE_SKIP_INSTALL_RPATH=ON \
	\
	-DQT_FEATURE_androiddeployqt=OFF \
	-DQT_FEATURE_avx2=OFF \
	-DQT_FEATURE_avx512bw=OFF \
	-DQT_FEATURE_avx512cd=OFF \
	-DQT_FEATURE_avx512dq=OFF \
	-DQT_FEATURE_avx512er=OFF \
	-DQT_FEATURE_avx512f=OFF \
	-DQT_FEATURE_avx512ifma=OFF \
	-DQT_FEATURE_avx512pf=OFF \
	-DQT_FEATURE_avx512vbmi2=OFF \
	-DQT_FEATURE_avx512vbmi=OFF \
	-DQT_FEATURE_avx512vl=OFF \
	-DQT_FEATURE_avx=OFF \
	-DQT_FEATURE_backtrace=OFF \
	-DQT_FEATURE_concurrent=OFF \
	-DQT_FEATURE_cups=OFF \
	-DQT_FEATURE_dbus=OFF \
	-DQT_FEATURE_eglfs=OFF \
	-DQT_FEATURE_fontconfig=OFF \
	-DQT_FEATURE_gif=OFF \
	-DQT_FEATURE_glib=OFF \
	-DQT_FEATURE_gtk3=OFF \
	-DQT_FEATURE_gui=OFF \
	-DQT_FEATURE_harfbuzz=OFF \
	-DQT_FEATURE_icu=OFF \
	-DQT_FEATURE_journald=OFF \
	-DQT_FEATURE_jpeg=OFF \
	-DQT_FEATURE_kms=OFF \
	-DQT_FEATURE_libinput=OFF \
	-DQT_FEATURE_libudev=OFF \
	-DQT_FEATURE_linuxfb=OFF \
	-DQT_FEATURE_opengl=OFF \
	-DQT_FEATURE_png=OFF \
	-DQT_FEATURE_printsupport=OFF \
	-DQT_FEATURE_sql_db2=OFF \
	-DQT_FEATURE_sql_ibase=OFF \
	-DQT_FEATURE_sql_mysql=OFF \
	-DQT_FEATURE_sql_oci=OFF \
	-DQT_FEATURE_sql_odbc=OFF \
	-DQT_FEATURE_sql_psql=OFF \
	-DQT_FEATURE_sql_sqlite=OFF \
	-DQT_FEATURE_sse2=OFF \
	-DQT_FEATURE_sse3=OFF \
	-DQT_FEATURE_sse4_1=OFF \
	-DQT_FEATURE_sse4_2=OFF \
	-DQT_FEATURE_ssse3=OFF \
	-DQT_FEATURE_syslog=OFF \
	-DQT_FEATURE_system_doubleconversion=OFF \
	-DQT_FEATURE_system_libb2=OFF \
	-DQT_FEATURE_system_pcre2=OFF \
	-DQT_FEATURE_system_zlib=OFF \
	-DQT_FEATURE_testlib=OFF \
	-DQT_FEATURE_tslib=OFF \
	-DQT_FEATURE_vaes=OFF \
	-DQT_FEATURE_widgets=OFF \
	-DQT_FEATURE_xcb=OFF \
	-DQT_FEATURE_zstd=OFF \
	\
	-DINPUT_intelcet=no \
	-DINPUT_opengl=no \
	\
	-DQT_USE_BUNDLED_BundledHarfbuzz=OFF \
	\
	-DQT_FEATURE_shared=OFF \
	-DQT_FEATURE_static=ON

# XXX qt-tools wants network
CMAKE_HOST_OPTIONS += \
	-DCMAKE_INSTALL_PREFIX=../Qt6 \
	-DQT_FEATURE_network=ON \
	-DQT_FEATURE_sql=OFF \
	-DQT_FEATURE_xml=ON \
	$(QT6_COMMON_OPTIONS)

CMAKE_OPTIONS += \
	-DCMAKE_SYSROOT=$(STAGING_DIR) \
	-DCMAKE_TOOLCHAIN_FILE=$(PKG_BUILD_DIR)/toolchain.cmake \
	\
	-DQT_FEATURE_gssapi=OFF \
	-DQT_HOST_PATH=$(HOST_BUILD_DIR)/../Qt6 \
	-DQT_QMAKE_TARGET_MKSPEC=devices/linux-entware-g++ \
	-DQT_FEATURE_dtls=ON \
	-DQT_FEATURE_network=ON \
	-DQT_FEATURE_openssl=ON \
	-DQT_FEATURE_openssl_hash=OFF \
	-DQT_FEATURE_openssl_runtime=ON \
	-DQT_FEATURE_openssl_linked=ON \
	-DQT_FEATURE_sql=ON \
	-DQT_FEATURE_ssl=ON \
	-DQT_FEATURE_xml=ON \
	\
	-DQT_FEATURE_getentropy=OFF \
	-DQT_FEATURE_precompile_header=OFF \
	-DQT_FEATURE_relocatable=OFF \
	-DQT_FEATURE_renameat2=OFF \
	-DQT_FEATURE_statx=OFF \
	-DINPUT_openssl=yes \
	\
	-DINSTALL_DATADIR=share/Qt6 \
	-DINSTALL_DESCRIPTIONSDIR=share/Qt6/modules \
	-DINSTALL_INCLUDEDIR=include/Qt6 \
	-DINSTALL_LIBEXECDIR=libexec \
	-DINSTALL_MKSPECSDIR=share/Qt6/mkspecs \
	-DINSTALL_PLUGINSDIR=lib/Qt6/plugins \
	$(QT6_COMMON_OPTIONS)

TARGET_CFLAGS += -pthread
TARGET_CXXFLAGS += -pthread
TARGET_LDFLAGS:=

define FixPreConfigure
	$(SED) 's,^QMAKE_CC\s*=.*,QMAKE_CC = $(HOSTCC_NOCACHE),; \
		s,^QMAKE_CXX\s*=.*,QMAKE_CXX = $(HOSTCXX_NOCACHE),' \
			$(PKG_BUILD_DIR)/mkspecs/common/g++-base.conf
	$(SED) 's,^QMAKE_CC\s*=.*,QMAKE_CC = $(TARGET_CC),; \
		s,^QMAKE_CXX\s*=.*,QMAKE_CXX = $(TARGET_CXX),; \
		s,@TARGET_CFLAGS@,$(TARGET_CFLAGS),g; \
		s,@TARGET_CXXFLAGS@,$(TARGET_CXXFLAGS),g' \
			$(PKG_BUILD_DIR)/mkspecs/devices/linux-entware-g++/qmake.conf
	$(SED) 's|@TARGET_CXXFLAGS@|$(TARGET_CXXFLAGS)|g; \
		s|@TARGET_LDFLAGS@|$(TARGET_LDFLAGS)|g; \
		s,@ARCH@,$(ARCH),g; \
		s,@TARGET_CROSS@,$(TARGET_CROSS),g; \
		s,@STAGING_DIR@,$(STAGING_DIR),g; \
		s,@TOOLCHAIN_DIR@,$(TOOLCHAIN_DIR),g' \
			$(PKG_BUILD_DIR)/toolchain.cmake
endef

Hooks/Configure/Pre += FixPreConfigure

define Package/qt6-core/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libQt6Core.so.* $(1)/opt/lib
endef

define Package/qt6-network/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libQt6Network.so.* $(1)/opt/lib
	# XXX wants plugins
	$(INSTALL_DIR) $(1)/opt/lib/Qt6
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/Qt6/plugins $(1)/opt/lib/Qt6
endef

define Package/qt6-sql/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libQt6Sql.so.* $(1)/opt/lib
endef

define Package/qt6-xml/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libQt6Xml.so.* $(1)/opt/lib
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,qt6-core))
$(eval $(call BuildPackage,qt6-network))
$(eval $(call BuildPackage,qt6-sql))
$(eval $(call BuildPackage,qt6-xml))
