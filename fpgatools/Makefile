
include $(TOPDIR)/rules.mk

PKG_NAME:=fpgatools
PKG_VERSION:=
PKG_REV:=HEAD
PKG_RELEASE:=1
PKG_INSTALL:=1

PKG_SOURCE:=$(PKG_NAME).tar.gz
PKG_SOURCE_URL:=git://github.com/Wolfgang-Spraul/fpgatools.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/fpgatools
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=fpgatools
	DEPENDS:=+libusb-compat +libftdi1
endef

define Package/fpgatools/description
fpgatools is a toolchain to program field-programmable gate arrays (FPGAs)
endef

TARGET_LDFLAGS += -L$(STAGING_DIR)/usr/lib

define Build/Compile
	$(call Build/Compile/fpgatools, fp2bit, bit2fp)
	$(MAKE_VARS) $(MAKE) -C $(PKG_BUILD_DIR)/mini-jtag $(MAKE_FLAGS) \
	DESTDIR="$(PKG_INSTALL_DIR)" \
	all install
endef

define Package/fpgatools/install

	$(INSTALL_DIR)	$(1)/usr/bin
	$(INSTALL_DIR)	$(1)/usr/lib

	$(INSTALL_BIN)	$(PKG_INSTALL_DIR)/usr/local/bin/fp2bit		$(1)/usr/bin
	$(INSTALL_BIN)	$(PKG_INSTALL_DIR)/usr/local/bin/bit2fp		$(1)/usr/bin
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/local/lib/libfpga-*	$(1)/usr/lib

endef

define Package/mini-jtag
	TITLE+=mini-jtag
	DEPENDS:=+libusb-compat +libftdi1
endef

define Package/mini-jtag/install
	$(CP)	$(STAGING_DIR)/usr/lib/libusb-0.1.so*		$(1)/usr/lib
	$(INSTALL_DIR)	$(1)/usr/bin
	$(INSTALL_BIN)	$(PKG_INSTALL_DIR)/usr/local/bin/mini-jtag	$(1)/usr/bin
endef

$(eval $(call BuildPackage,fpgatools))
$(eval $(call BuildPackage,mini-jtag))
