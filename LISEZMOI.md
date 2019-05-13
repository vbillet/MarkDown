# Script md.php
[![GitHub version](https://badge.fury.io/gh/vbillet%2FMarkDown.svg)](https://badge.fury.io/gh/vbillet%2FMarkDown)<br/>
Ce script PHP a pour but de permettre le rendu de fichiers MarkDown (.md) en utilisant Apache et PHP. Tant que le script est installé, vous pouvez demander des fichiers .md à votre navigateur, et les voir correctement formatés en HTML. Par exemple : http://www.mywebsite.com/README.md sera affiché au format HTML au lieu du texte plein.
## Installation
Téléchargez le script sur [GitHub.com](https://github.com/vbillet/MarkDown).
Il suffit de copier les fichiers **md.php**, **w3.css**, **hcode.css** et **hcode.js** à la _racine du site_.
La documentaion est disponible sur [le site du projet](https://vbillet.github.io/MarkDown/).
## Configuration
Pour utiliser ce script, il faut ajouter dans le fichier **httpd.conf**, dans la section **Virtual Host**, les lignes suivantes: 
````    
RewriteEngine on
RewriteRule (.*)\.md$ /md.php?f=$1
````
### Exemple : 
Cet exemple montre une configucation de localweb complète avec l'URL rewriting activé pour les fichiers .md.
````xml
## Virtualhost localweb
<VirtualHost 192.168.1.x>
	DocumentRoot "C:/Work/PHP"
	ServerName 192.168.1.x
	
	RewriteEngine on
	RewriteRule (.*)\.md$ /md.php?f=$1
	
	<Directory "C:/Work/PHP">
		Options FollowSymLinks Indexes ExecCGI
		AllowOverride All
		Order allow,deny
		Allow from all
		Require all granted
	</Directory>
</VirtualHost>
````
Pour plus d'informations sur l'URL Rewriting avec Apache, consultez : [Le site de développez.com](https://apache.developpez.com/cours/urlrewriting/) ou [le site de Apache](https://httpd.apache.org/docs/trunk/fr/mod/mod_rewrite.html#rewriterule).
## Utilisation dans PHP
Vous pouvez aussi utiliser **md.php** dans vos scripts PHP pour obtenir le rendu HTML d'une chaine caractère.
Il vous faut, en tout premier lieu, intégrer dans la section **head** du document HTML les lignes suivantes : 
````html
<head>
	<link rel="stylesheet" href="/w3.css">
	<link rel="stylesheet" href="/hcode.css">
	<script src="/hcode.js"></script>
	<script>hljs.initHighlightingOnLoad();</script>
</head>
````
Ensuite, il suffit d'utiliser le script de la manière suivante :
````php
require_once "md.php";
$Markdown = new Markdown();
$htmlMarkDown = $Markdown->text("Hello, this is a **MarkDown** string.");
echo($htmlMarkDown);
````
## Références
Ce script est basé sur les scripts suivants : 
* [MarkDown Parser in PHP](https://parsedown.org/)
* [W3Shcool CSS Framework](https://www.w3schools.com/w3css/default.asp)
* [highlight.js](https://highlightjs.org/)

Consultez ces sites pour plus d'informations sur le fonctionnement de **md.php**.
