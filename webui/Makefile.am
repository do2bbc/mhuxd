hdfdir = $(HDFDIR)
webuistaticdir = $(WEBUIDIR)/static
webuicsdir = $(WEBUIDIR)/cs
webuisveltedir = $(WEBUIDIR)/svelte

# The Svelte UI is built ahead of time on the maintainer's machine and its
# compiled output is committed under svelte/dist. Packaging therefore needs
# neither npm nor network access (e.g. offline builders like Launchpad PPAs).
# Run "make svelte-ui-build" to regenerate svelte/dist after editing the UI.
SVELTE_SRC_DIR = $(abs_srcdir)/svelte
SVELTE_DIST_DIR = $(srcdir)/svelte/dist
SVELTE_NPM ?= npm

dist_hdf_DATA = \
    hdf/mhuxd.hdf

dist_webuistatic_DATA = \
	static/monda400.woff \
	static/monda700.woff \
	static/mhuxd.css \
	static/arrow-down.png \
	static/arrow-up.png \
	static/big_bullet.gif \
	static/checkmark.gif \
	static/contexthelp2.gif \
	static/dot.gif \
	static/error.png \
	static/Green1.png \
	static/Green2.png \
	static/Green3.png \
	static/mhuxd-logo.gif \
	static/mhuxd.png \
	static/navtab2-left.gif \
	static/navtab2-right.gif \
	static/navtab2-sel-left.gif \
	static/navtab2-sel-right.gif \
	static/nocheckmark.gif \
	static/note.gif \
	static/Red1.png \
	static/section-end-corner2.gif \
	static/section-end-horiz.gif \
	static/section-end-vert.gif \
	static/section-start-corner2.gif \
	static/section-start-horiz.gif \
	static/section-start-vert.gif \
	static/stop.gif \
	static/warning.gif \
	static/Yellow.png \
	static/scrollfix.js

dist_webuics_DATA = \
	cs/messages.cs \
	cs/messages_box.cs \
	cs/audio_mk1.cs \
	cs/audio_mk2.cs \
	cs/audio_mk2_opts.cs \
	cs/audio_mk2r_r1.cs \
	cs/audio_mk2r_r2.cs \
	cs/daemon_ports.cs \
	cs/daemon_settings.cs \
	cs/display_cfg.cs \
	cs/display_ev.cs \
	cs/home.cs \
	cs/home_summary.cs \
	cs/keyer_audiosw.cs \
	cs/keyer_aux.cs \
	cs/keyer_display.cs \
	cs/keyer_fsk.cs \
	cs/keyer_mode.cs \
	cs/keyer_ptt.cs \
	cs/keyer_radio.cs \
	cs/keyer_summary.cs \
	cs/keyer_winkey.cs \
	cs/left_menu.cs \
	cs/macros.cs \
	cs/mode_cfg.cs \
	cs/pageheader.cs \
	cs/ptt_cfg.cs \
	cs/ptt_footsw.cs \
	cs/sectionheader.cs \
	cs/serial_cfg.cs \
	cs/sidetone_cfg.cs \
	cs/summary_cfg.cs \
	cs/winkey_cfg.cs \
	cs/sm_antsw_outputs.cs \
	cs/sm_antsw_settings.cs \
	cs/sm_antsw_ant_list.cs \
	cs/sm_antsw_vr_list.cs \
	cs/sm_antsw_grp_list.cs \
	cs/sm_antsw_band_list.cs \
	cs/sm_antsw_load_store.cs

EXTRA_DIST = \
	svelte/package.json \
	svelte/package-lock.json \
	svelte/vite.config.js \
	svelte/svelte.config.js \
	svelte/jsconfig.json \
	svelte/index.html \
	svelte/src \
	svelte/dist \
	hdf/mhuxd.hdf

# Install the pre-built Svelte UI. No npm/network access required.
# Normalize permissions after copying: the committed sources may be read-only
# (e.g. under "make distcheck"), and cp -R would otherwise carry that over and
# break uninstall.
install-data-local:
	$(MKDIR_P) "$(DESTDIR)$(webuisveltedir)"
	cp -R "$(SVELTE_DIST_DIR)"/. "$(DESTDIR)$(webuisveltedir)"/
	chmod -R u+rwX,go+rX,go-w "$(DESTDIR)$(webuisveltedir)"

uninstall-local:
	@rm -rf "$(DESTDIR)$(webuisveltedir)"

# Maintainer convenience target: rebuild svelte/dist from sources. This needs
# npm and network access and is only ever run on the developer's machine, never
# at package build time. The resulting svelte/dist is committed to the repo.
svelte-ui-build:
	cd "$(SVELTE_SRC_DIR)" && "$(SVELTE_NPM)" install && "$(SVELTE_NPM)" run build

.PHONY: svelte-ui-build