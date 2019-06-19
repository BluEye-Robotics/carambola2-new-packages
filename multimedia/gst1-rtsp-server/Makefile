include $(TOPDIR)/rules.mk

PKG_NAME:=gst1-rtsp-server
PKG_VERSION:=1.16.0
PKG_RELEASE:=1

PKG_MAINTAINER:= Sindre Hansen <sindre.hansen@blueye.no>

PKG_SOURCE:=gst-rtsp-server-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://gstreamer.freedesktop.org/src/gst-rtsp-server
PKG_HASH:=0f51f9879556c0950203c766b09a1b62f1f25b17f9a7d516e01b13ecf93c8858

PKG_LICENSE:=LGPLv2 GPLv2
PKG_LICENSE_FILES:=COPYING.LIB COPYING

PKG_BUILD_DIR:=$(BUILD_DIR)/gst-rtsp-server-$(PKG_VERSION)

PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

GST_VERSION:=1.0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/gst1-rtsp-server
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=Gstreamer RTSP Server
	URL:=https://gstreamer.freedesktop.org/modules/gst-rtsp-server.html
	DEPENDS:=+glib2 +gstreamer1 +gst1-plugins-base
endef

define Package/gst1-rtsp-server/description
  RTSP server library based on GStreamer
endef

CONFIGURE_ARGS += \
	--disable-Bsymbolic \
	--disable-fatal-warnings \
	--disable-glib-asserts \
	--disable-gobject-cast-checks \
	--disable-gtk-doc-html \
	--enable-gettext=no

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/gstreamer-rtsp-server-$(GST_VERSION).pc $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libgstrtspserver-$(GST_VERSION).so* $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libgstrtspserver-$(GST_VERSION).la $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/include/gstreamer-$(GST_VERSION)
	$(CP) $(PKG_INSTALL_DIR)/usr/include/gstreamer-$(GST_VERSION)/* $(1)/usr/include/gstreamer-$(GST_VERSION)
endef

define Package/gst1-rtsp-server/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/examples/.libs/test-launch $(1)/usr/bin/gst-rtsp-launch
endef

$(eval $(call BuildPackage,gst1-rtsp-server))
