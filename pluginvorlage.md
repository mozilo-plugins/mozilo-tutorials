# Pluginvorlage

Die folgende Pluginvorlage stellt ein mögliches Grundgerüst und oft verwendete Funktionen eines moziloCMS 2.0 Plugins zur Verfügung.

## index.php

```php
<?php if(!defined('IS_CMS')) die();
 
/**
 * Plugin:   pluginVorlage
 * @author:  Autor (Mailadresse)
 * @version: v0.x.jjjj-mm-dd
 * @license: GPL
 *
**/
 
class pluginVorlage extends Plugin {
 
  public $admin_lang;
  private $cms_lang;
 
  function getContent($value) {
 
    global $CMS_CONF;
    global $syntax;
 
    $this->cms_lang = new Language(PLUGIN_DIR_REL . 'pluginVorlage/lang/cms_language_' . $CMS_CONF->get('cmslanguage') . '.txt');
 
    // get language labels
    $label = $this->cms_lang->getLanguageValue('label');
 
    // get params
    $values = explode('|', $value);
 
    // get conf
    $conf = array(
      'text' => $this->settings->get('text'),
      'textarea' => $this->settings->get('textarea'),
      'password' => $this->settings->get('password'),
      'check' => $this->settings->get('check'),
      'radio' => $this->settings->get('radio'),
      'select' => $this->settings->get('select')
    );
 
    // include jquery and pluginVorlage javascript
    $syntax->insert_jquery_in_head('jquery');
    $syntax->insert_in_head('<script type="text/javascript" src="' . URL_BASE . PLUGIN_DIR_NAME . '/pluginVorlage/js/pluginVorlage.js"></script>');
 
    // initialize return content
    $content = '';
 
    // do something awesome here!
 
    return $content;
  }
 
 
  function getConfig() {
 
    $config = array();
 
    // text
    $config['text']  = array(
      'type' => 'text',
      'description' => $this->admin_lang->getLanguageValue('config_text'),
      'maxlength' => '100',
      'size' => '5',
      'regex' => "/^[0-9]{1,2}$/",
      'regex_error' => $this->admin_lang->getLanguageValue('config_text_error')
    );
 
    // textarea
    $config['textarea']  = array(
      'type' => 'textarea',
      'description' => $this->admin_lang->getLanguageValue('config_textarea'),
      'cols' => '10',
      'rows' => '10',
      'regex' => "/^[0-9]{1,2}$/",
      'regex_error' => $this->admin_lang->getLanguageValue('config_textarea_error')
    );
 
    // password
    $config['password']  = array(
      'type' => 'password',
      'description' => $this->admin_lang->getLanguageValue('config_password'),
      'maxlength' => '100',
      'size' => '5',
      'regex' => "/^[0-9]{3,5}$/",
      'regex_error' => $this->admin_lang->getLanguageValue('config_password_error'),
      'saveasmd5' => true
    );
 
    // checkbox
    $config['checkbox']  = array(
      'type' => 'checkbox',
      'description' => $this->admin_lang->getLanguageValue('config_checkbox')
    );
 
    // radio
    $config['radio']  = array(
      'type' => 'radio',
      'description' => $this->admin_lang->getLanguageValue('config_radio'),
      'descriptions' => array(
        'blau' => 'Blau',
        'rot' => 'Rot',
        'gruen' => 'Grün'
      )
    );
 
    // select
    $config['select']  = array(
      'type' => 'select',
      'description' => $this->admin_lang->getLanguageValue('config_select'),
      'descriptions' => array(
        'blau' => 'Blau',
        'rot' => 'Rot',
        'gruen' => 'Grün'
      ),
      'multiple' => false
    );
 
    return $config;
  }
 
 
  function getInfo() {
 
    global $ADMIN_CONF;
 
    $this->admin_lang = new Language(PLUGIN_DIR_REL . 'pluginVorlage/lang/admin_language_' . $ADMIN_CONF->get('language') . '.txt');
 
    $info = array(
      // plugin name and version
      '<b>pluginVorlage</b> v0.x.jjjj-mm-dd',
      // moziloCMS version
      '2.0',
      // short description, only <span> and <br /> are allowed
      $this->admin_lang->getLanguageValue('description'), 
      // author
      'Autor',
      // documentation url
      'http://www.url.de',
      // plugin tag for select box when editing a page, can be emtpy
      array(
        '{pluginVorlage|parameter}' => $this->admin_lang->getLanguageValue('placeholder'),
      )
    );
 
    return $info;
  }
}
 
?>
```

## Erklärung
`Zeile 1:` Sicherheitsabfrage, damit der Plugincode nur im moziloCMS Kontext ausgeführt  
`Zeile 2-8:` Optionale Plugininformationen  
`Zeile 13-14:` Deklaration der Sprachvariablen

`Zeile 21+124:` Zuweisung der Sprachvariablen zu den entsprechenden Sprachdateien.  
`Zeile 24:` Auslesen der Sprachdateien durch Ansprechen des Sprachobjektes unter Verwendung des gewünschten Indexes  
`Zeile 27:` Falls Parameter im Plugintag verwendet werden sollen, werden diese hier ausgelesen und in ein Array gespeichert.  
`Zeile 30-37:` Auslesen der Backendkonfiguration, falls gesetzt  
`Zeile 40-41:` Falls jQuery oder Javascript verwendet wird, kann dieses im Header eingebunden werden - jQuery bringt moziloCMS 2.0 von Haus aus mit  
`Zeile 44-48:` Die eigentliche Programmlogik - hier wird die Ausgabe des Plugins zurückgegeben

`Zeile 54:` Initialisierung des Konfigurations-Array - falls keine Konfiguration gewünscht, hier einfach das Array leer lassen  
`Zeile 57-64:` einzeiliges Textfeld  
`Zeile 57-64:` einzeiliges Textfeld  
`Zeile 67-74:` mehrzeiliges Textfeld  
`Zeile 87-81:` Checkbox  
`Zeile 94-102:` Radiobuttons  
`Zeile 105-114:` Auswahlfeld

`Zeile 126:` Plugininformationen zur Anzeige im Backend
