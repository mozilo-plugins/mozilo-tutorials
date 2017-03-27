# Plugin erstellen

Die folgenden Beschreibungen zum Erstellen von Plugins beziehen sich auf moziloCMS 2.0.

## Die Verzeichnisstruktur

Für ein lauffähiges Plugin braucht es lediglich einen Ordner mit dem Namen des Plugins, in welchem sich eine Datei `index.php` befindet. Damit wäre die minimale Verzeichnisstruktur bereits gegeben. Zusätzlich dazu ist es noch möglich, eine für das Plugin spezifische CSS-Datei, Dateien für mehrsprachige Ausgabe und Javascript Dateien zu erstellen. Daraus ergibt sich folgende Dateistruktur:

![plugin_verzeichnis_struktur](https://cloud.githubusercontent.com/assets/5441654/24345632/563532e8-12d1-11e7-9bc4-5adcf118fe01.jpg)

Wenn man für das Plugin keine eigenen Stylesheets oder Javascriptdateien benötigt, lässt man entsprechende Ordner oder Dateien einfach weg. Soll die Stylesheet-Datei automatisch vom System eingebunden werden, ist es wichtig, dass die Datei `plugin.css` heißt. Im Beispiel sieht man Sprachdateien für Front- und Backend, jeweils in Deutsch und Englisch.

## Die index.php

Die `index.php` stellt die Schnittstelle zwischen Plugin und moziloCMS dar. Sie besteht grundlegend aus einer Klasse `meinPlugin` (der Klassenname muss identisch mit dem root-Ordnernamen des Plugins sein), welche die Klasse `Plugin` erweitert und folgenden 3 Funktionien:

### getContent($value)
Die Funktion `getContent()` ist der Kern des Plugins. Hier liegt die Programmlogik (oder wird hier eingebunden) und die Rückgabe der Funktion ist die Ausgabe des Plugins. Außerdem werden hier optional über das Plugin-Tag übergebene Parameter (`$value`) verarbeitet oder die im Backend gesetzte Konfiguration ausgelesen.

### getConfig()
Die Funktion `getConfig()` realisiert die Backendadministration des Plugins. Hier werden Textfelder, Auswahlfelder, Checkboxen und andere Formularelemente definiert, welche im Backend für das Plugin gesetzt werden können. Hier kann auch ein leeres Array zurückgegeben werden, wenn keine Konfiguration im Backend gebraucht wird.

### getInfo()
Die Funktion `getInfo()` gibt Plugininformationen wie Pluginname, -version, Autor, Beschreibung, Downloadlink und vom Plugin bereitgestellte Tags an.

### Beispiel
Das folgende Beispielplugin gibt den aktuellen Wochentag aus.

```php
<?php if(!defined('IS_CMS')) die();
 
class wochenTag extends Plugin {
 
   function getContent($value) {
      $wochentag = date("l");
      return 'Heute ist ' . $wochentag;
   }
 
   function getConfig() {
      $config = array();
      return $config; 
   }
 
   function getInfo() {
      $info = array(
         // Plugin-Name + Version
         '<b>wochenTag</b> v0.0.2020-12-24',
         // moziloCMS-Version
         '2.0',
         // Kurzbeschreibung nur <span> und <br /> sind erlaubt
         'Das Plugin wochenTag gibt den aktuellen Wochentag aus.', 
         // Name des Autors
         'Mein Name',
         // Docu-URL
         'http://www.documentation.de',
         // Platzhalter für die Selectbox in der Editieransicht, kann leer sein
         array(
            '{wochenTag}' => 'Gibt den aktuellen Wochentag aus',
         )
      );
      return $info;
   }
}
?>
```

## Konfiguration

In der Funktion `getConfig()` sind verschiedene Formularelemente möglich, welche im Backend gesetzt werden können. Diese sind im [moziloCMS Entwicklerportal](http://www.mozilo.de/Entwicklerportal/Plugins%20programmieren/Details.html) dokumentiert, oder können der [Pluginvorlage](pluginvorlage.md) entnommen werden.

## Installation

Um das erstellte Plugin zu testen, muss es in den Ordner `plugins` von moziloCMS z.B. per FTP kopiert werden. moziloCMS erkennt das Plugin genau dann, wenn...
... der Pluginordner eine Datei `index.php` enthält
... die `index.php` eine PHP-Klasse enthält, die genauso heißt die der Pluginordner
... diese Klasse die 3 oben beschriebenen Funktionen enthält
... benötigte Schreibrechte gesetzt sind.

Sind diese Vorrausetzungen erfüllt, so ist das Plugin im Backend unter dem Menüpunkt `Plugins` aufgeführt. Per Klick auf `Aktivieren` ist das Plugin aktiv und kann verwendet und getestet werden.

## Entwicklung

Um Plugins in moziloCMS zu entwickeln braucht es also nicht viel. An sich reicht ein einfacher Texteditor zum Bearbeiten der Dateien und ein FTP-Programm zum Hochladen der geänderten Dateien.

## Siehe auch

- http://www.mozilo.de/Entwicklerportal/Plugins programmieren.html
