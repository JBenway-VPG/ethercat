#------------------------------------------------------------------------------
#
#  Makefile.am
#
#  IgH EtherCAT master
#
#  Copyright (C) 2006-2022  Florian Pose, Ingenieurgemeinschaft IgH
#
#  This file is part of the IgH EtherCAT Master.
#
#  The IgH EtherCAT Master is free software; you can redistribute it and/or
#  modify it under the terms of the GNU General Public License version 2, as
#  published by the Free Software Foundation.
#
#  The IgH EtherCAT Master is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General
#  Public License for more details.
#
#  You should have received a copy of the GNU General Public License along
#  with the IgH EtherCAT Master; if not, write to the Free Software
#  Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
#
#------------------------------------------------------------------------------

SUBDIRS = init.d sysconfig

sbin_SCRIPTS = ethercatctl

dist_sysconf_DATA = ethercat.conf

script_templates = \
	ethercatctl.in \
	ethercat.service.in

EXTRA_DIST = \
	$(script_templates) \
	ethercat.bash_completion \
	ifup-eoe.sh

CLEANFILES = \
	ethercatctl \
	ethercat.service

if HAVE_SYSTEMD
systemdsystemunit_DATA = ethercat.service
endif

completionsdir = $(datadir)/bash-completion/completions
completions_DATA = ethercat.bash_completion

install-data-hook:
	cd $(DESTDIR)$(completionsdir); \
    mv ethercat.bash_completion ethercat

uninstall-hook:
	cd $(DESTDIR)$(completionsdir); \
    rm ethercat

# Any precious variable used inside script_templates should appear here
expand_script = $(SED) \
	-e 's,[@]VERSION[@],$(VERSION),g' \
	-e 's,[@]bindir[@],$(bindir),g' \
	-e 's,[@]sbindir[@],$(sbindir),g' \
	-e 's,[@]sysconfdir[@],$(sysconfdir),g'

ethercatctl: $(srcdir)/ethercatctl.in Makefile
	$(expand_script) < $< > $@

ethercat.service: $(srcdir)/ethercat.service.in Makefile
	$(expand_script) < $< > $@

#------------------------------------------------------------------------------
