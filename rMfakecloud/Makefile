include $(TOPDIR)/rules.mk

PKG_NAME:=rMfakecloud
PKG_VERSION:=0.0.5
PKG_RELEASE:=1

PKG_LICENSE:=GPLv2
PKG_MAINTAINER:=Leo_Zhao

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Build/Prepare
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=This is a replacement of the reMarkable cloud
	PKGARCH:=all
endef

define Package/$(PKG_NAME)/description
	This is a replacement of the reMarkable cloud
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) ./fakecloud $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./fakecloud.init $(1)/etc/init.d/fakecloud
	$(INSTALL_DIR) $(1)/etc/nginx
	$(INSTALL_BIN) ./fakecloud.conf $(1)/etc/nginx/conf.d
	$(INSTALL_DIR) $(1)/etc/dnsmasq.d
	$(INSTALL_DATA) ./reMarkable.conf $(1)/etc/dnsmasq.d
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
