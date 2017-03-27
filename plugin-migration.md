# Plugin Migration

Von moziloCMS 1.12 zu 2.0 hat sich eine ganze Menge getan - leider sind damit auch viele Plugins, die unter 1.12 lauffähig sind, inkompatibel zu 2.0. Im Folgenden beschreibe ich schrittweise, wie die Migration eines Plugins aus 1.12 nach 2.0 realisiert werden kann:

## 1. Kopieren und Dateinamen anpassen

Als Erstes sollte der komplette Ordner des zu migrierenden Plugins kopiert werden. Eine Umbenennung ist nicht zwingend notwendig, da sowohl altes als auch neues Plugin ja niemals in der gleichen moziloCMS Instanz existieren. 

Anschließend kann man die Datei `plugin.conf` (sofern vorhanden) löschen, da diese unter 2.0 automatisch generiert wird. 

Wenn ein Ordner `sprachen` o.ä. mit Sprachdateien vorhanden ist, welche vom Dateityp `.conf` sind, müssen diese in `.txt` Dateien umbenannt werden.

## 2. Anpassen der index.php

Nachdem die Vorbereitungen von Schritt 1 getroffen sind, muss nun die `index.php` direkt angepasst werden.

Direkt nach dem öffnenden PHP-Tag ganz oben folgende Bedingung setzen (wenn nicht schon vorhanden):

```php
if (!defined('IS_CMS')) {
    die();
}
```

Wenn mehrere Sprachen genutzt werden können, werden diese nicht mehr als globale Variable definiert, sondern public/private ganz oben in der Plugin-Klasse, z.B.:

```php
class pluginName extends Plugin {
 
    public $admin_lang;
    private $cms_lang;
 
    function getContent($value) {
    ...
```

Um Instanzen der Sprachobjekte zu erstellen, NICHT mehr `new Properties` verwenden, sondern nur noch `new Language`. z.B.:

```php
$this->_cms_lang = new Language(
    $this->PLUGIN_SELF_DIR
    . 'lang/cms_language_'
    . $CMS_CONF->get('cmslanguage')
    . '.txt'
);

$this->admin_lang = new Language(
    $this->PLUGIN_SELF_DIR
    . 'lang/admin_language_'
    . $ADMIN_CONF->get('language')
    . '.txt'
);
```

Zum Auslesen der Sprache NICHT mehr `getLanguageValue0()`, `getLanguageValue1()`, etc. verwenden, sondern:

```php
$this->cms_lang->getLanguageValue('...', $param1, $param2)
$this->admin_lang->getLanguageValue('...', $param1, $param2)
```

Die Parameter können optional gesetzt werden.

Die Funktion `getRequestParam()` wird nicht mehr verwendet, stattdessen:

```php
getRequestValue()
```

Als Letztes muss man noch prüfen, ob folgende Konstanten ohne das Dollarzeichen `$` gesetzt sind:

```php
CHARSET
CMS_DIR_NAME
CONTENT_DIR_NAME
CONTENT_FILES_DIR_NAME
PLUGIN_DIR_NAME
GALLERIES_DIR_NAME
PREVIEW_DIR_NAME
EXT_PAGE
EXT_HIDDEN
EXT_DRAFT
EXT_LINK
BASE_DIR
BASE_DIR_CMS
CONTENT_DIR_REL
PLUGIN_DIR_REL
URL_BASE
CAT_REQUEST
PAGE_REQUEST
```

## 3. Hochladen und Testen

Hat man alle Änderungen vorgenommen, kann das Plugin hochgeladen, aktiviert und getestet werden. Möglicherweise sind weitere Schritte und Anpassungen nötig.
