# SPDX-License-Identifier: GPL-2.0-only

include $(TOPDIR)/rules.mk

PKG_NAME:=rathole
PKG_VERSION:=0.5.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://github.com/rathole-org/rathole.git
PKG_MIRROR_HASH:=ba938c0ff885e0c4e0356635d4c8e126618b816f1bee12e6406cbd23a7dd2db5
PKG_SOURCE_DATE:=2025-07-29
PKG_SOURCE_VERSION:=5a9dd6d939744859af322aeff7fd60f7483a68bc

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=rust/host
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include ../../../../feeds/packages/lang/rust/rust-package.mk

define Package/rathole
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A lightweight and high-performance reverse proxy for NAT traversal
  DEPENDS:=$(RUST_ARCH_DEPENDS) +libopenssl
  URL:=https://github.com/rathole-org/rathole
endef

define Package/rathole/description
  A lightweight and high-performance reverse proxy for NAT
  traversal, written in Rust.
endef

define Package/rathole/conffiles
/etc/rathole/
endef

define Package/rathole/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/rathole $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/etc/init.d/rathole $(1)/etc/init.d/
	$(INSTALL_DIR) $(1)/etc/rathole
endef

$(eval $(call RustBinPackage,rathole))
$(eval $(call BuildPackage,rathole))
