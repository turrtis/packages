# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Fusion CCTV, Inc.

include $(TOPDIR)/rules.mk

PKG_NAME:=mediamtx
PKG_VERSION:=1.17.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/bluenviron/mediamtx/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=skip

PKG_MAINTAINER:=turrtis
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DIR:=$(BUILD_DIR)/mediamtx-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/bluenviron/mediamtx
GO_PKG_TAGS += rpicamera

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/package-defaults.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/mediamtx
  SECTION:=net
  CATEGORY:=Network
  TITLE:=mediamtx
  URL:=https://github.com/bluenviron/mediamtx
  DEPENDS:=$(GO_ARCH_DEPENDS) +libfreetype
endef

define Package/mediamtx/description
  MediaMTX (formerly rtsp-simple-server) is a ready-to-use and
  zero-dependency real-time media server and media proxy that allows to
  publish, read, proxy, record and playback video and audio streams.
endef

define Build/Configure
	$(call GoPackage/Build/Configure)
	echo "v$(PKG_VERSION)" > $(PKG_BUILD_DIR)/internal/core/VERSION
	(cd $(PKG_BUILD_DIR) && go generate ./internal/servers/hls)
	mkdir -p $(PKG_BUILD_DIR)/internal/staticsources/rpicamera/mtxrpicam_32
	mkdir -p $(PKG_BUILD_DIR)/internal/staticsources/rpicamera/mtxrpicam_64
	touch $(PKG_BUILD_DIR)/internal/staticsources/rpicamera/mtxrpicam_32/dummy.bin
	touch $(PKG_BUILD_DIR)/internal/staticsources/rpicamera/mtxrpicam_64/dummy.bin
endef

# - Set MAKE_PATH to build rpicamera protocol extension in the Configuration step.
# - Manually call do `go generate` as setting $(GO_PKG_GO_GENERATE)
#   does not make a good job.

$(eval $(call GoPackage,mediamtx))
$(eval $(call BuildPackage,mediamtx))
