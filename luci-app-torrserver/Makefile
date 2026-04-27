include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-torrserver
PKG_VERSION:=2.0.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION)_all.ipk
PKG_SOURCE_URL:=https://github.com/turrtis/luci-app-torrserver/releases/download/v$(PKG_VERSION)/
PKG_HASH:=4c02be6de0be05de0d2d53cb798af38d838f481365e38dd01c87377f3963daed

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-torrserver
  SECTION:=luci
  CATEGORY:=LuCI
  SUBMENU:=3. Applications
  TITLE:=LuCI for TorrServer
  DEPENDS:=+torrserver-upx +luci-base +rpcd +rpcd-mod-file +ucode
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	tar -xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR)
	tar -xzf $(PKG_BUILD_DIR)/data.tar.gz -C $(PKG_BUILD_DIR)
	rm -f $(PKG_BUILD_DIR)/control.tar.gz $(PKG_BUILD_DIR)/data.tar.gz $(PKG_BUILD_DIR)/debian-binary
endef

define Build/Compile
endef

define Package/luci-app-torrserver/install
	$(INSTALL_DIR) $(1)/usr $(1)/www
	$(CP) $(PKG_BUILD_DIR)/usr/* $(1)/usr/
	$(CP) $(PKG_BUILD_DIR)/www/* $(1)/www/
endef

$(eval $(call BuildPackage,luci-app-torrserver))
