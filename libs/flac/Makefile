#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=flac
PKG_VERSION:=1.3.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://downloads.xiph.org/releases/flac/
PKG_MD5SUM:=b9922c9a0378c88d3e901b234f852698
PKG_MAINTAINER:=Ted Hess <thess@kitschensync.net>

PKG_INSTALL:=1

PKG_LICENSE:=GFDL-1.2 GPL-2 LGPL-2.1 BSD-3-Clause
PKG_LICENSE_FILES:=README COPYING.FDL COPYING.GPL COPYING.LGPL COPYING.Xiph

PKG_FIXUP:=autoreconf
PKG_REMOVE_FILES:=autogen.sh aclocal.m4

include $(INCLUDE_DIR)/package.mk

define Package/libflac
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Free Lossless Audio Codec library
  URL:=https://xiph.org/flac
endef

CONFIGURE_ARGS += \
	--disable-cpplibs \
	--disable-sse \
	--disable-3dnow \
	--disable-altivec \
	--disable-doxgen-docs \
	--disable-local-xmms-plugin \
	--disable-xmms-plugin \
	--disable-ogg \
	--disable-oggtest \
	--disable-debug \
	--enable-static \

TARGET_CFLAGS += $(FPIC)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/include/FLAC \
		$(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/libFLAC.{a,so*,la} \
		$(1)/opt/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/opt/lib/pkgconfig/* \
		$(1)/opt/lib/pkgconfig/

	$(INSTALL_DIR) $(1)/opt/share/aclocal/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/opt/share/aclocal/* \
		$(1)/opt/share/aclocal/
endef

define Package/libflac/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libFLAC.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libflac))
