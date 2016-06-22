#
# Copyright (C) 2015-2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk


PKG_NAME:=libmraa
PKG_VERSION:=1.0.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/8devices/mraa.git
PKG_SOURCE_VERSION:=9116655da79cc7d6432b25927a495e22221f86fd
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_BUILD_DEPENDS:=node python/host swig/host node/host
CMAKE_INSTALL:=1

PKG_MAINTAINER:=John Crispin <blogic@openwrt.org>
PKG_LICENSE:=LGPL-2.1
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

CMAKE_OPTIONS=-DBUILDARCH=$(CONFIG_ARCH) \
	-DENABLEEXAMPLES=1 \
	-DNODEJS_EXECUTABLE=$(STAGING_DIR)/host/bin/node \
	-DNODEJS_INCLUDE_DIRS=$(STAGING_DIR)/usr/include/node/ \
	-DSWIG_EXECUTABLE=$(STAGING_DIR)/host/bin/swig \

TARGET_CFLAGS+=-I$(STAGING_DIR)/usr/include/node

define Package/libmraa/Default
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libstdcpp
  TITLE:=Intel IoT lowlevel IO library
  URL:=https://github.com/intel-iot-devkit/mraa
endef

define Package/libmraa/Default/description
  Libmraa is a C/C++ library with bindings to Java, Python and JavaScript to interface
with the IO on Galileo, Edison & other platforms, with a structured and sane API where
port names/numbering matches the board that you are on. Use of libmraa does not tie you
to specific hardware with board detection done at runtime you can create portable code
that will work across the supported platforms.
endef

define Package/libmraa
  $(call Package/libmraa/Default)
  TITLE:=Intel IoT lowlevel IO C/C++ library
  DEPENDS:=+libstdcpp +libjson-c @!arc @!armeb @!powerpc
endef

define Package/libmraa/description
$(call Package/libmraa/Default/description)

This package contains the C/C++ libraries.
endef

define Package/libmraa-node
  $(call Package/libmraa/Default)
  TITLE:=Intel IoT lowlevel IO Node.js library
  DEPENDS:=+libmraa +node
endef

define Package/libmraa-node/description
$(call Package/libmraa/Default/description)

This package contains the Node.js libraries.
endef

define Package/libmraa-python
  $(call Package/libmraa/Default)
  TITLE:=Intel IoT lowlevel IO Python library
  DEPENDS:=+libmraa +python-light
endef

define Package/libmraa-python/description
$(call Package/libmraa/Default/description)

This package contains the Python libraries.
endef

define Package/libmraa-python3
  $(call Package/libmraa/Default)
  TITLE:=Intel IoT lowlevel IO Python3 library
  DEPENDS:=+libmraa +python3-light
endef

define Package/libmraa-python3/description
$(call Package/libmraa/Default/description)

This package contains the Python3 libraries.
endef

define Package/libmraa-nodejs
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libmraa +node
  TITLE:=Intel IoT lowlevel IO library nodejs bindings
endef

define Package/libmraa-python
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libmraa +python
  TITLE:=Intel IoT lowlevel IO library python bindings
endef

define Package/libmraa-examples
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libmraa +libmraa-nodejs +libmraa-python
  TITLE:=Intel IoT lowlevel IO library examples
endef

define Package/libmraa/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/libmraa.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/mraa/examples/mraa-gpio $(1)/usr/bin/
endef

MRAA_EXAMPLES_C := \
	analogin_a0 blink-io blink_onboard cycle-pwm3 gpio_read6 hellomraa i2c_HMC5883L \
	isr_pin6 mmap-io2 mraa-i2c spi_max7219 spi_mcp4261 uart uart_ow

MRAA_EXAMPLES_CPP := AioA0 I2c-compass Iio-dummy Isr-pin6 Pwm3-cycle Spi-pot Uart UartOW

define Package/libmraa-examples/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(foreach example, $(MRAA_EXAMPLES_C),	\
		$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/mraa/examples/$(example) $(1)/usr/bin/;)
	$(foreach example, $(MRAA_EXAMPLES_CPP),	\
		$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/mraa/examples/c++/$(example) $(1)/usr/bin/;)
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/mraa/examples/python/*.py $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/mraa/examples/javascript/*.js $(1)/usr/bin/
endef

define Package/libmraa-nodejs/install
	$(INSTALL_DIR) $(1)/usr/lib/node/mraa
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/node_modules/mraa/* $(1)/usr/lib/node/mraa/
endef

define Package/libmraa-python/install
	$(INSTALL_DIR) $(1)/usr/lib/python2.7/site-packages
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/python2.7/site-packages/* $(1)/usr/lib/python2.7/site-packages/
endef

$(eval $(call BuildPackage,libmraa))
$(eval $(call BuildPackage,libmraa-nodejs))
$(eval $(call BuildPackage,libmraa-python))
$(eval $(call BuildPackage,libmraa-examples))

