# remove titlebar form firefox

There is a bug in deepin that the titlebar in firefox wont disappear even if it is turned off. It is described in this [issue](https://github.com/linuxdeepin/developer-center/issues/1460).

To fix this it is sufficient to create a modified .desktop file for firefox, which activates **client side decoration**: ``Exec=env MOZ_GTK_TITLEBAR_DECORATION=client /opt/firefox/firefox %u``

```ini
[Desktop Entry]
Comment=Browse the World Wide Web
GenericName=Web Browser
X-GNOME-FullName=Firefox Web Browser
Exec=env MOZ_GTK_TITLEBAR_DECORATION=client /opt/firefox/firefox %u
Terminal=false
X-MultipleArgs=false
Type=Application
Icon=/opt/firefox/browser/chrome/icons/default/default128.png
Categories=Network;WebBrowser;
MimeType=text/html;text/xml;application/xhtml+xml;application/xml;application/vnd.mozilla.xul+xml;application/rss+xml;application/rdf+xml;image/gif;image/jpeg;image/png;x-scheme-handler/http;x-scheme-handler/https;
StartupWMClass=Firefox
StartupNotify=true
```