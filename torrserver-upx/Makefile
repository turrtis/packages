include $(TOPDIR)/rules.mk

PKG_NAME:=torrserver-upx
PKG_VERSION:=141
PKG_RELEASE:=1

PKG_ARCH:=aarch64_cortex-a53
PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION)_$(PKG_ARCH).ipk
PKG_SOURCE_URL:=https://github.com/turrtis/luci-app-torrserver/releases/download/MatriX.$(PKG_VERSION)/
PKG_HASH:=7533378495f7d0d3fe76d41bb897c44136843fb7684c7870a0ac752935904a7b

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=torrserver-upx binary for $(PKG_ARCH)
  DEPENDS:=+libc +libpthread
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	tar -xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR)
	tar -xzf $(PKG_BUILD_DIR)/data.tar.gz -C $(PKG_BUILD_DIR)
	rm -f $(PKG_BUILD_DIR)/control.tar.gz $(PKG_BUILD_DIR)/data.tar.gz $(PKG_BUILD_DIR)/debian-binary
endef

define Build/Compile
	# Binary package, no compilation needed
endef

define Package/torrserver-upx/install
	$(INSTALL_DIR) $(1)/usr $(1)/etc
	$(CP) $(PKG_BUILD_DIR)/usr/* $(1)/usr/
	$(CP) $(PKG_BUILD_DIR)/etc/* $(1)/etc/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
