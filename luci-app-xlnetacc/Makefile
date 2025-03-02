include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-xlnetacc
PKG_VERSION:=1
PKG_RELEASE:=2

PKG_LICENSE:=GPLv2
PKG_MAINTAINER:=Sense <sensec@gmail.com>

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=luci
	CATEGORY:=LuCI
	SUBMENU:=3. Applications
	TITLE:=LuCI Support for XLNetAcc
	PKGARCH:=all
	DEPENDS:=+jshn +curl +openssl-util +luci-compat
endef

define Package/$(PKG_NAME)/description
	LuCI Support for XLNetAcc.
endef

define Build/Prepare
	$(foreach po,$(wildcard ${CURDIR}/files/luci/i18n/*.po), \
		po2lmo $(po) $(PKG_BUILD_DIR)/$(patsubst %.po,%.lmo,$(notdir $(po)));)
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/conffiles
	/etc/config/xlnetacc
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/i18n
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/xlnetacc.*.lmo $(1)/usr/lib/lua/luci/i18n/
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/controller
	$(INSTALL_DATA) ./files/luci/controller/*.lua $(1)/usr/lib/lua/luci/controller/
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/cbi
	$(INSTALL_DATA) ./files/luci/model/cbi/*.lua $(1)/usr/lib/lua/luci/model/cbi/
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/view/xlnetacc
	$(INSTALL_DATA) ./files/luci/view/xlnetacc/*.htm $(1)/usr/lib/lua/luci/view/xlnetacc/
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/root/etc/config/xlnetacc $(1)/etc/config/xlnetacc
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/root/etc/init.d/xlnetacc $(1)/etc/init.d/xlnetacc
	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface
	$(INSTALL_BIN) ./files/root/etc/hotplug.d/iface/95-xlnetacc $(1)/etc/hotplug.d/iface/95-xlnetacc
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/root/etc/uci-defaults/* $(1)/etc/uci-defaults/
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) ./files/root/usr/bin/xlnetacc.sh $(1)/usr/bin/xlnetacc.sh
	$(INSTALL_DIR) $(1)/usr/share/rpcd/acl.d
	$(INSTALL_DATA) ./files/acl.d/* $(1)/usr/share/rpcd/acl.d/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
