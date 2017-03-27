# Backend Styles

Aus verschiedenen Gründen kann es sinnvoll sein, das moziloCMS Backend Design zu verändern. Ist man beispielsweise Administrator mehrerer moziloCMS Instanzen, so kann man die Backends schon an der Login-Seite sofort voneinander unterscheiden und muss nicht erst die Domain überprüfen. Auch für Redakteure ist es deutlich intuitiver, wenn das Backend z.B. der gleichen Farbgebung wie das Frontend folgt.

## Theme erstellen

moziloCMS nutzt jQuery Themes, welche auf [jqueryui.com](http://jqueryui.com/themeroller/) erstellt und gedownloaded werden können. Dazu kann man im ThemeRoller mithilfe der linken Konfigurationsbox sein eigenes Theme zusammenklicken. Sowohl Grundeinstellungen zu Fonts, Farben und Links als auch spezifischere Elemente wie Formularelemente, Hinweis- oder Fehlermeldungen und vieles mehr kann beliebig angepasst werden.

Hat man alle gewünschten Anpassungen vorgenommen, kann das Theme gedownloaded werden. Der Klick auf den Download-Button führt zum Download Builder, der per Default alle jQuery Elemente angehakt hat. Oben sollte unter _Version_ die aktuelle (stable) jQuery Version gewählt werden. Unten kann unter _Theme Folder Name_ noch ein Name für das Theme gesetzt werden, beispielsweise `mozilo-blue`. Der Name `mozilo` sollte hier vermieden werden, da das aktuelle Backend Theme in moziloCMS diesen Namen trägt.

## Theme installieren

Um nun ein jQuery Theme für das moziloCMS Backen zu installieren, kann folgendermaßen vorgegangen werden:

- Die gedownloadede Archivdatei entpacken und zum Ordner `css/` navigieren. In diesem Ordner sollte sich ein Ordner mit dem zuvor vergebenen Namen `mozilo-blue` befinden.
- Dieser Ordner muss nun auf den Server nach `<moziloroot>/admin/css/` hochgeladen werden (z.B. mithilfe eines FTP-Clienten wie FileZilla). Anschließend sollten sich in dem Ordner `<moziloroot>/admin/css/` auf dem Server die beiden Ordner `mozilo` und `mozilo-blue` befinden.
- Als letztes muss im Admin-Template noch der Pfad angepasst werden. Dazu bearbeitet man die Datei `<moziloroot>/admin/admin_template.php`:  
In Zeile 79 sollte die alte Zuweisung der CSS-Datei stehen:

      $html .= '<link type="text/css" rel="stylesheet" href="' . URL_BASE . ADMIN_DIR_NAME . '/css/mozilo/jquery-ui-1.9.2.custom.css" />';

  Diese Zeile duplizieren und auskommentieren (z.B. mit `#` am Zeilenanfang)
Die neue Zeile 80 nun an den neuen Pfad anpassen, z.B.:

      $html .= '<link type="text/css" rel="stylesheet" href="' . URL_BASE . ADMIN_DIR_NAME . '/css/mozilo-blue/jquery-ui-1.10.3.custom.min.css" />';

  Empfehlenswert ist an dieser Stelle die .min Variante der CSS-Datei zu wählen, da diese die für schnelleres Laden optimierte Version ist. Schaut man in mozilo-blue rein, sieht man, welche CSS-Dateien zur Verfügung stehen und wie sie heißen.
- Das wars. Jetzt noch den Browsercache leeren und schauen, ob das Backend wie gewünscht aussieht.

## Siehe auch

- [jqueryui.com/themeroller](http://jqueryui.com/themeroller/)
- [Thread im moziloCMS Forum](http://www.mozilo.de/forum/index.php/topic,3497.msg17070.html)
