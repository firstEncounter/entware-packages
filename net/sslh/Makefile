#
# Copyright (C) 2009-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sslh
PKG_VERSION:=v1.17
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://rutschle.net/tech/
PKG_MD5SUM:=1fc3ada4bafaca5a9786cc1431f48ed4
PKG_LICENSE:=GPL-2.0+
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

define Package/sslh
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing and Redirection
  TITLE:=SSL/SSH multiplexer
  URL:=http://rutschle.net/tech/sslh.shtml
  PKG_MAINTAINER:=Jonathan McCrohan <jmccrohan@gmail.com>
endef

define Package/sslh/conffiles
/etc/config/sslh
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		USELIBCONFIG= \
		USELIBWRAP= \
		USELIBPCRE= \
		all
endef

define Package/sslh/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sslh-fork $(1)/opt/sbin/sslh
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) files/S14$(PKG_NAME) $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,sslh))
