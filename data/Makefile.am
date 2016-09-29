## Process this file with automake to produce Makefile.in

SUBDIRS = icons

desktopdir = $(datadir)/applications
desktop_in_files = glade.desktop.in.in
desktop_DATA = $(desktop_in_files:.desktop.in.in=.desktop)
@INTLTOOL_DESKTOP_RULE@

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = gladeui-2.0.pc

@INTLTOOL_XML_RULE@
appdatadir = $(datadir)/appdata
appdata_DATA = $(appdata_in_files:.xml.in=.xml)
appdata_in_files = glade.appdata.xml.in

EXTRA_DIST = 				\
	$(appdata_in_files)		\
	$(desktop_in_files)		\
	glade.wxs.in			\
	gladeui-2.0.pc.in

CLEANFILES =	 			\
	$(desktop_DATA)			\
	$(pkgconfig_DATA)		\
	$(appdata_DATA)

if PLATFORM_WIN32

glade-$(WIXL_ARCH)-$(VERSION).msi: glade.wxs
	$(AM_V_GEN)DESTDIR=`mktemp -d` &&				\
	make -C $(top_builddir) install DESTDIR=$$DESTDIR >/dev/null &&	\
	find $$DESTDIR | wixl-heat -p $$DESTDIR$(prefix)/		\
	    --component-group CG.glade --var var.DESTDIR		\
	    --directory-ref=INSTALLDIR > glade-files.wxs &&		\
	wixl -D SourceDir=$(prefix)					\
             -D DESTDIR=$$DESTDIR$(prefix)				\
             --arch $(WIXL_ARCH)					\
             -o $@							\
	     $< glade-files.wxs &&				\
	rm -rf $$DESTDIR glade-files.wxs

msi: glade-$(WIXL_ARCH)-$(VERSION).msi

CLEANFILES +=					\
	glade-$(WIXL_ARCH)-$(VERSION).msi

endif
