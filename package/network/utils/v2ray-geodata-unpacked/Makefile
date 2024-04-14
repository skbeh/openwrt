# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021-2022 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=v2ray-geodata-unpacked
PKG_RELEASE:=1

PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Tianling Shen <cnsztl@immortalwrt.org>

PKG_BUILD_DEPENDS:=v2dat/host

include $(INCLUDE_DIR)/package.mk

GEODATA_VER:=202603182227

GEOIP_FILE:=geoip.dat.$(GEODATA_VER)
define Download/geoip
  URL:=https://github.com/Loyalsoldier/v2ray-rules-dat/releases/download/$(GEODATA_VER)/
  URL_FILE:=geoip.dat
  FILE:=$(GEOIP_FILE)
  HASH:=e48b925d985d7bf33cfee76f309241af0f1779699963b69363dec2c4740041d1
endef

GEOSITE_FILE:=geosite.dat.$(GEODATA_VER)
define Download/geosite
  URL:=https://github.com/Loyalsoldier/v2ray-rules-dat/releases/download/$(GEODATA_VER)/
  URL_FILE:=geosite.dat
  FILE:=$(GEOSITE_FILE)
  HASH:=08686bdab2aaec2beabe97baa23c6812a4383a4833e5a3877be712e66a81a4c3
endef

define Package/v2ray-geodata-unpacked/template
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  URL:=https://www.v2fly.org
  PKGARCH:=all
endef

define Package/v2ray-geoip-unpacked
  $(call Package/v2ray-geodata-unpacked/template)
  TITLE:=GeoIP List for V2Ray
  VERSION:=$(GEODATA_VER)-r$(PKG_RELEASE)
  LICENSE:=CC-BY-SA-4.0
endef

define Package/v2ray-geosite-unpacked
  $(call Package/v2ray-geodata-unpacked/template)
  TITLE:=Geosite List for V2Ray
  VERSION:=$(GEODATA_VER)-r$(PKG_RELEASE)
  LICENSE:=MIT
endef

define Build/Prepare
	$(call Build/Prepare/Default)
ifneq ($(CONFIG_PACKAGE_v2ray-geoip-unpacked),)
	$(call Download,geoip)
endif
ifneq ($(CONFIG_PACKAGE_v2ray-geosite-unpacked),)
	$(call Download,geosite)
endif
endef

define Build/Compile
endef

define Package/v2ray-geoip-unpacked/install
	cd $(PKG_BUILD_DIR) && $(STAGING_DIR_HOSTPKG)/bin/v2dat unpack geoip $(DL_DIR)/$(GEOIP_FILE)

	$(INSTALL_DIR) $(1)/usr/share/v2ray
	cd $(PKG_BUILD_DIR) && for file in geoip.dat_*.txt; do \
		$(INSTALL_DATA) "$$$$file" "$(1)/usr/share/v2ray/$$$${file/geoip.dat_/geoip_}"; \
	done
endef

define Package/v2ray-geosite-unpacked/install
	cd $(PKG_BUILD_DIR) && $(STAGING_DIR_HOSTPKG)/bin/v2dat unpack geosite $(DL_DIR)/$(GEOSITE_FILE)

	$(INSTALL_DIR) $(1)/usr/share/v2ray
	cd $(PKG_BUILD_DIR) && for file in geosite.dat_*.txt; do \
		$(INSTALL_DATA) "$$$$file" "$(1)/usr/share/v2ray/$$$${file/geosite.dat_/geosite_}"; \
	done
endef

$(eval $(call BuildPackage,v2ray-geoip-unpacked))
$(eval $(call BuildPackage,v2ray-geosite-unpacked))
