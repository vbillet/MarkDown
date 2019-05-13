# md.php Script
[![GitHub version](https://badge.fury.io/gh/vbillet%2FMarkDown.svg)](https://badge.fury.io/gh/vbillet%2FMarkDown)<br/>
This PHP script aims to render MarkDown (.md) files using Apache and PHP. As long as the script is installed, you can request .md files from your browser, and see them correctly formatted in HTML. For instance : http://www.mywebsite.com/README.md will be displayed in HTML instead of full text.

## Installation
Download this script on [GitHub.com](https://github.com/vbillet/MarkDown).
Just copy the **md.php**, **w3.css**, **hcode.css** and **hcode.js** files to the root of the site.
Documentation is available on [project's website](https://vbillet.github.io/MarkDown/).
## Configuration
To use this script, add the following lines to the **httpd.conf** file in the **Virtual Host** section:
````    
RewriteEngine on
RewriteRule (.*)\.md$ /md.php?f=$1
````
### Example : 
This example shows a localweb configucation complete with URL rewriting enabled for .md files.
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
For more information on the Rewriting URL with Apache, see : [Apache WebSite](https://httpd.apache.org/docs/trunk/fr/mod/mod_rewrite.html#rewriterule).
## Using with PHP
You can also use **md.php** in your PHP scripts to get the HTML rendering of a character string.
First of all, you need to include in the **head** section of the HTML document the following lines:
````html
<head>
	<link rel="stylesheet" href="/w3.css">
	<link rel="stylesheet" href="/hcode.css">
	<script src="/hcode.js"></script>
	<script>hljs.initHighlightingOnLoad();</script>
</head>
````
Then, just use the script as follows:
````php
require_once "md.php";
$Markdown = new Markdown();
$htmlMarkDown = $Markdown->text("Hello, this is a **MarkDown** string.");
echo($htmlMarkDown);
````
## References
This script is based on the following scripts:
* [MarkDown Parser in PHP](https://parsedown.org/)
* [W3Shcool CSS Framework](https://www.w3schools.com/w3css/default.asp)
* [highlight.js](https://highlightjs.org/)

Check these sites for more information on how **md.php** works.
