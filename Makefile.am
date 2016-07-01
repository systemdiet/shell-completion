ACLOCAL_AMFLAGS = ${ACLOCAL_FLAGS}
AM_MAKEFLAGS = --no-print-directory

SUBDIRS = .

rootprefix=@rootprefix@
rootlibexecdir=$(rootprefix)/lib/systemd
bashcompletiondir=@bashcompletiondir@
zshcompletiondir=@zshcompletiondir@

EXTRA_DIST =
CLEANFILES =

substitutions = \
		'|rootlibexecdir=$(rootlibexecdir)|'

SED_PROCESS = \
	$(AM_V_GEN)$(MKDIR_P) $(dir $@) && \
	$(SED) $(subst '|,-e 's|@,$(subst =,\@|,$(subst |',|g',$(substitutions)))) \
		< $< > $@

DISTCHECK_CONFIGURE_FLAGS = \
	--with-rootprefix=$$dc_install_base \
	--with-bashcompletiondir=$$dc_install_base/$(bashcompletiondir) \
	--with-zshcompletiondir=$$dc_install_base/$(zshcompletiondir)

dist_bashcompletion_DATA = \
	bash/journalctl \
	bash/systemd-analyze \
	bash/systemd-cat \
	bash/systemd-cgls \
	bash/systemd-cgtop \
	bash/systemd-delta \
	bash/systemd-detect-virt \
	bash/systemd-run \
	bash/udevadm \
	bash/kernel-install

nodist_bashcompletion_DATA = \
	bash/systemctl

dist_zshcompletion_DATA = \
	zsh/_journalctl \
	zsh/_udevadm \
	zsh/_kernel-install \
	zsh/_systemd-analyze \
	zsh/_systemd-run \
	zsh/_sd_hosts_or_user_at_host \
	zsh/_sd_outputmodes \
	zsh/_sd_unit_files \
	zsh/_systemd-delta \
	zsh/_systemd

nodist_zshcompletion_DATA = \
	zsh/_systemctl

EXTRA_DIST += \
	bash/systemctl.in \
	zsh/_systemctl.in

CLEANFILES += \
	$(nodist_bashcompletion_DATA) \
	$(nodist_zshcompletion_DATA)

dist_zshcompletion_DATA += \
	zsh/_systemd-tmpfiles

dist_bashcompletion_DATA += \
	bash/loginctl

dist_zshcompletion_DATA += \
	zsh/_loginctl \
	zsh/_systemd-inhibit

bash/%: bash/%.in
	$(SED_PROCESS)

zsh/%: zsh/%.in
	$(SED_PROCESS)
