#
# Copyright (C) 2014 OpenWrt.org  
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# updated to work with latest source from abrasive
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libsoxr
PKG_VERSION:=0.1.1
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://git.code.sf.net/p/soxr/code
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_LICENSE:=LGPL-2.1
PKG_LICENSE_FILES:=LICENCE

PKG_FIXUP:=libtool
PKG_REMOVE_FILES:=autogen.sh

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libsoxr
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=The SoX Resampler library
  URL:=http://sourceforge.net/projects/soxr/
  MAINTAINER:=Mike Brady <mikebrady@eircom.net>
  DEPENDS:= +libpthread
endef

define Package/libsoxr/description
  The SoX Resampler library
  High quality, one-dimensional sample-rate conversion library
endef

CMAKE_OPTIONS:= -DBUILD_SHARED_LIBS=OFF -DBUILD_TESTS=0 -DBUILD_EXAMPLES=0
CMAKE_OPTIONS+= -DHAVE_WORDS_BIGENDIAN_EXITCODE=$(if $(CONFIG_BIG_ENDIAN),0,1)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_BUILD_DIR)/src/soxr.h $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/src/*.a $(1)/opt/lib/
endef

define Package/libsoxr/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/src/*.a $(1)/opt/lib/
endef


$(eval $(call BuildPackage,libsoxr))
