include $(TOPDIR)/rules.mk

PKG_NAME:=aic8800
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/goecho/aic8800_linux_drvier.git
PKG_SOURCE_BRANCH:=main
PKG_MIRROR_HASH:=skip

include $(INCLUDE_DIR)/kernel.mk

define Package/aic8800-firmware
    SECTION:=firmware
    CATEGORY:=Firmware
    TITLE:=Firmware for Aicsemi aic8800
    DEPENDS:=
endef

define Package/aic8800-firmware/description
    This package contains the firmware files for the Aicsemi aic8800 Wi-Fi chip.
endef

define KernelPackage/aic8800
  SUBMENU:=Wireless Drivers
  TITLE:=Driver for Aicsemi Aic8800
  DEPENDS:=+kmod-cfg80211 +kmod-mac80211 +aic8800-firmware
  FILES:=$(PKG_BUILD_DIR)/aic8800_bsp.ko
  AUTOLOAD:=$(call AutoLoad,50,aic8800_bsp)
endef

define KernelPackage/aic8800/description
  This is the kernel module for the Aicsemi aic8800 Wi-Fi chip.
endef

define Build/Compile
    $(MAKE) -C $(PKG_BUILD_DIR) \
        CONFIG_AIC_IW_SUPPORT=y \
        CONFIG_AIC_P2P_SUPPORT=y \
        CONFIG_AIC_AP_SUPPORT=y \
        KVER="$(LINUX_VERSION)" \
        KSRC="$(LINUX_DIR)" \
        DESTDIR="$(PKG_BUILD_DIR)"
endef

define Package/aic8800-firmware/install
    $(INSTALL_DIR) $(1)/lib/firmware/aic8800
    $(CP) $(PKG_BUILD_DIR)/firmware/aic8800/* $(1)/lib/firmware/aic8800/
endef

$(eval $(call BuildPackage,aic8800-firmware))
$(eval $(call KernelPackage,aic8800))
