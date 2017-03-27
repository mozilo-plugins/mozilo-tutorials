# Sprachumschalter

Der folgende Inhalt bezieht sich auf moziloCMS 1.12, kann analog aber auch für moziloCMS 2.0 verwendet werden.

## Verwendung

Will man auf einer moziloCMS Website Inhalte mehrsprachig präsentieren, so kann man dies mit dem i18n ("Internationalization") Plugin realisieren. Hat man das Plugin installiert und aktiviert, kann mit folgendem Snippet dem Benutzer die Möglichkeit geboten werden, die Sprachen komfortabel zu wechseln. Dabei ist immer der Sprachlink deaktiviert, dessen Sprache grad aktiv ist.
Natürlich können statt den Wörtern auch entsprechende Bilder (z.B. Fahnen) gesetzt werden.

## Zweisprachig
Im folgenden Beispielcode kann zwischen Deutsch und Englisch gewechselt werden:

```html
<div class="languages">
    {i18n|de|Deutsch | {i18n|switch_en|English}}
    {i18n|en|{i18n|switch_de|Deutsch} | English}
</div>
```

## Dreisprachig
Im folgenden Beispielcode kann zwischen Deutsch, Englisch und Französisch gewechselt werden:

```html
<div id="languages">
  {i18n|de|Deutsch | {i18n|switch_en|English} | {i18n|switch_fr|Français}}
  {i18n|en|{i18n|switch_de|Deutsch} | English | {i18n|switch_fr|Français}}
  {i18n|fr|{i18n|switch_de|Deutsch} | {i18n|switch_en|English} | Français}
</div>
```

## Siehe auch
[software.azett.com](http://software.azett.com/index.php?cat=moziloCMS-Plugins&page=i18n)
[mozilo.de/pluginarchiv](http://www.mozilo.de/forum/index.php?action=media;sa=item;in=147)
