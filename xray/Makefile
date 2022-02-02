include $(TOPDIR)/rules.mk

PKG_NAME:=xray-core
PKG_VERSION:=1.5.3
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/XTLS/Xray-core.git
PKG_SOURCE_VERSION:=d51db9469eaa96ac11d0099e398d0acd587fb15d

PKG_MAINTAINER:=Leo Zhao
PKG_LICENSE:=MPL-2.0
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DIR:=$(BUILD_DIR)/Xray-core-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/xtls/xray-core
GO_PKG_BUILD_PKG:=github.com/xtls/xray-core/main
GO_PKG_LDFLAGS:=-s -w
GO_PKG_LDFLAGS_X:= \
	$(GO_PKG)/core.build=OpenWrt \
	$(GO_PKG)/core.version=$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/xray-LZMA
  TITLE:=A platform for building proxies to bypass network restrictions
  SECTION:=net
  CATEGORY:=Network
  URL:=https://github.com/XTLS/Xray-core
  DEPENDS:=$(GO_ARCH_DEPENDS) +ca-bundle
endef

define Package/xray-LZMA/description
  Xray, Penetrates Everything. Also the best v2ray-core, with XTLS support. Fully compatible configuration.
  It secures your network connections and thus protects your privacy.
endef

define Build/Compile
	$(eval GO_PKG_BUILD_PKG:=$(GO_PKG)/main)
	$(call GoPackage/Build/Compile)
	mv -f $(GO_PKG_BUILD_BIN_DIR)/main $(GO_PKG_BUILD_BIN_DIR)/xray
	$(STAGING_DIR_HOST)/bin/upx --lzma --best $(GO_PKG_BUILD_BIN_DIR)/xray || true
endef

define Package/xray-LZMA/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/xray $(1)/usr/bin
endef

$(eval $(call BuildPackage,xray-LZMA))
