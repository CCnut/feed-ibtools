# Copyright (C) 2020 CCnut
#
# This is free software, licensed under the GNU General Public License v2.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=mstflint
PKG_VERSION:=4.15.0
PKG_RELEASE:=1

PKG_SOURCE:=mstflint-$(PKG_VERSION)-$(PKG_RELEASE).tar.gz
PKG_SOURCE_URL:=https://github.com/Mellanox/mstflint/releases/download/v$(PKG_VERSION)-$(PKG_RELEASE)
PKG_HASH:=3b3f6c6d8962513ed923fdb2da3d03a5e5e6827038ba16047881fdc413270b32

PKG_FIXUP:=autoreconf
PKG_REMOVE_FILES:=autogen.sh
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_FIXUP:=patch-libtool

include $(INCLUDE_DIR)/package.mk

define Package/mstflint
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=tools for mellanox manufactured cards
  DEPENDS:=+libsqlite3 +libopenssl +libstdcpp +rdma-core
endef

define Package/mstflint/description
This package contains a burning tool and diagnostic tools for Mellanox manufactured HCA/NIC cards. It also provides access to the relevant source code.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)/missing-headers/sys
	$(CP) ./files/pci.h $(PKG_BUILD_DIR)/missing-headers/sys/
	$(call Build/Prepare/Default)
endef

TARGET_CFLAGS += -D_GNU_SOURCE -isystem $(PKG_BUILD_DIR)/missing-headers

CONFIGURE_ARGS += \
	--enable-shared

define Build/Configure
	$(call Build/Configure/Default,$(CONFIGURE_ARGS))
endef

define Package/mstflint/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/share
	$(CP) $(PKG_INSTALL_DIR)/usr/share/* $(1)/usr/share/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))