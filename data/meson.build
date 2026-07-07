datadir = get_option('datadir')
app_id = 'org.xmms2.abraca'
icondir = join_paths(datadir, 'icons', 'hicolor')

# Application icon, installed into the hicolor theme under the app-id so that
# the desktop entry (Icon=org.xmms2.abraca) and the runtime window icon
# (Gtk.Window.set_icon_name in abraca-window.vala) resolve.
foreach size : ['16', '32', '128', '192']
  install_data('abraca-@0@.png'.format(size),
    install_dir : join_paths(icondir, '@0@x@0@'.format(size), 'apps'),
    rename : app_id + '.png',
  )
endforeach

install_data('abraca.svg',
  install_dir : join_paths(icondir, 'scalable', 'apps'),
  rename : app_id + '.svg',
)

# Desktop entry (validated at install time by gnome.post_install / d-f-u).
desktop_file = app_id + '.desktop'
install_data(desktop_file,
  install_dir : join_paths(datadir, 'applications'),
)

desktop_file_validate = find_program('desktop-file-validate', required : false)
if desktop_file_validate.found()
  test('validate-desktop', desktop_file_validate,
    args : [files(desktop_file)],
    suite : 'data',
  )
endif

# AppStream metadata.
metainfo_file = app_id + '.metainfo.xml'
install_data(metainfo_file,
  install_dir : join_paths(datadir, 'metainfo'),
)

appstreamcli = find_program('appstreamcli', required : false)
if appstreamcli.found()
  test('validate-metainfo', appstreamcli,
    args : ['validate', '--no-net', '--pedantic', files(metainfo_file)],
    suite : 'data',
  )
endif

# Man page.
install_man('abraca.1')
