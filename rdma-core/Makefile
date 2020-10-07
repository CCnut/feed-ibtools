# Copyright (C) 2020 CCnut
#
# This is free software, licensed under the GNU General Public License v2.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=rdma-core
PKG_VERSION:=31.0

PKG_SOURCE:=rdma-core-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/linux-rdma/rdma-core/releases/download/v$(PKG_VERSION)
PKG_HASH:=51ae9a3ab81cd6834436813fafc310c8b7007feae9d09a53fdd5c169e648d50b

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/rdma-core
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=RDMA Core Userspace Libraries and Daemons
  DEPENDS:=+libnl-core +libnl-genl +libnl-nf +libnl-route +kmod-mlx4-core +kmod-mlx5-core
endef

define Package/rdma-core/description
This is the userspace components for the Linux Kernel's drivers/infiniband subsystem.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
endef

CMAKE_INSTALL:=1
CMAKE_OPTIONS += -DNO_MAN_PAGES=1

define Build/Configure
	$(call Build/Configure/Default)
endef

define Package/rdma-core/install
	$(INSTALL_DIR) $(1)
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
