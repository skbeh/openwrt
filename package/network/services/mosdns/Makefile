# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=mosdns
PKG_VERSION:=5.3.4
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/maoxikun/mosdns
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2026-03-12
PKG_SOURCE_VERSION:=a6f80902757f4d1352f64041cc54dbd7e5ebd7e8
PKG_MIRROR_HASH:=2b4530ab71c73cb79ee97d1eee78f7ad29f9f598e6f7e333208c7c736694dc56

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Tianling Shen <cnsztl@immortalwrt.org>

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16

GO_PKG:=github.com/IrineSistiana/mosdns
GO_PKG_LDFLAGS_X:=main.version=v$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include ../../../../feeds/packages/lang/golang/golang-package.mk

define Package/mosdns
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE:=A plug-in DNS forwarder/splitter
  URL:=https://github.com/IrineSistiana/mosdns
  DEPENDS:=$(GO_ARCH_DEPENDS) +ca-bundle
endef

define Package/mosdns/conffiles
/etc/mosdns/
endef

define Package/mosdns/install
	$(call GoPackage/Package/Install/Bin,$(1))

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/scripts/openwrt/mosdns-init-openwrt $(1)/etc/init.d/mosdns

	$(INSTALL_DIR) $(1)/etc/mosdns
endef

$(eval $(call GoBinPackage,mosdns))
$(eval $(call BuildPackage,mosdns))
