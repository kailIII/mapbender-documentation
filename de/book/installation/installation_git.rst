.. _installation_git:

Git-basierte Installation
[4444444444444444444444444]


Wenn Sie sich an der Mapbender3-Entwicklung beteiligen möchten oder aus anderen Gründen die Git Repositories für Mapbender3 verwenden, folgen Sie dieser Anleitung statt des normalen Downloads. Diese Anleitung basiert auf Ubuntu 12.04.  Für andere Distributionen benötigen Sie vielleicht spezielle Pakete wie z.B. sphinx-common.

Prüfen Sie zuerst die `Systemvoraussetzungen <systemrequirements.html>`_.

Für die Git-basierte Installation benötigen Sie:

* git     - schauen Sie sich das Dokument `Quick primer on using Git <../../../en/book/development/git.html>`_ an, um mit Git vertraut zu werden.
* cURL    - kommandozeilen basiertes Tool für die Übertragung von Daten über URL Syntax,unterstützt HTTP, HTTPS und mehr.
* pear    - PHP Erweiterung und Anwendungs-Repository.
* Phing   - `Phing <http://www.phing.info/>`_ ist nicht GNU make; es ist ein  PHP Projekt Build System oder Build-Werkzeug basierend auf Apache Ant.
* php5-dev - Und natürlich die Dateien zur Entwicklung von PHP5-Modulen.


Klonen des Repositories
[555555555555555555555555]

Klonen ist einfach, geben Sie das folgende Kommando auf Ihrer Shell ein:

.. code-block:: bash

    git clone https://github.com/mapbender/mapbender-starter.git mapbender3
    cd mapbender3

Entwickler, die Zugriff auf den Code haben möchten, müssen die SSH-URL verwenden: git@github.com:mapbender/mapbender-starter


Zu einem Tag eines Mapbender3 Releases wechseln
[5555555555555555555555555555555555555555555555]

Um mit einer Release Version von Mapbender3 zu arbeiten, wechseln Sie bitte zu dem spezifischen Tag. Zum Beispiel für Version 3.0.5.0: 

.. code-block:: bash

    git tag -l
    git checkout v3.0.5.0


Submodule abrufen
[5555555555555555]

Die Starter-Applikation enthält nicht die Mapbender3 bundles, diese sind in einem eigenen Repository gespeichert und werden als Submodule in das Starter-Repository eingefügt. Rufen Sie das folgende Kommando im root-Verzeichnis ihres geklonten Repositories auf.

.. code-block:: bash

    git submodule update --init --recursive


cURL
====

Das build-System benutzt cURL, um einige Remote-Komponenten abzurufen. Dazu müssen Sie das cURL-Kommandozeilen-Werkzeug installieren:

.. code-block:: yaml

	sudo apt-get install curl

.. _phing:


Build-Management mit Phing
[555555555555555555555555555]


Das Build-Management wird mit Phing vorgenommen, welches die Pear-Bibliothek benötigt. Zunächst muss Pear installiert werden.  Hier wird ein Debian-basiertes System verwendet:


.. code-block:: yaml

    sudo apt-get install php-pear


Dann muss Pear gezeigt werden, wie ein Autodiscover seiner Repositories erzeugt wird.  Vorsichtshalber wird ein Update von Pear gemacht.


.. code-block:: yaml

    sudo pear config-set auto_discover 1
    sudo pear upgrade-all
      Enable full APC compatibility [yes] : yes
      Enable internal debugging in APCu [no] : yes 


Dann wird Phing installiert:


.. code-block:: yaml

    sudo pear channel-discover pear.phing.info 
    sudo pear install phing/phing


Composer und PHPUnit
[6666666666666666666]

PHPUnit wird über den Composer mitgeliefert. Die Build-Skripte  benötigen weitere Abhängigkeiten, um Unit-Tests durchzuführen, die Dokumentation zu generieren und die Installationspakete zu erstellen.

Sobald Sie die unten aufgeführten Abhängigkeiten installiert haben, können Sie sich über die folgende Eingabe einen Überblick über die verfügbaren Aufgaben verschaffen:

.. code-block:: yaml

   phing -l


Daher muss zuerst der Composer: für die Laufzeit-Abhängigkeiten, wie
Symfony und Doctrine installieren werden (weitere Information unter http://getcomposer.org/download/):

.. code-block:: yaml

    cd application
    curl -sS https://getcomposer.org/installer | php


Erzeugen Sie eine Konfigurationsdatei mit Namen parameters.yml. Kopieren Sie dazu die Datei application/app/config/parameters.yml.dist.

.. code-block:: bash

  cp app/config/parameters.yml.dist app/config/parameters.yml


Zur Anpassung der parameters.yml lesen Sie bitte das Kapitel `Anpassen der Konfigurationsdatei <configuration.html#anpassen-der-konfigurationsdatei>`_.

Laden Sie anschließend die Laufzeit-Umgebungen wie Symfony und Doctrine:

.. code-block:: yaml

  ./composer.phar update 



Die nächsten Schritte der Installation
[5555555555555555555555555555555555555]

Folgen Sie nun den Schritten, die unter `Installation <installation_ubuntu.html>`_ beschrieben werden:

**Hinweis:** Beachten Sie dabei, dass Mapbender3 in dem git-basierten Aufbau über eines zusätzliches Verzeichnis *application* verfügt (mapbender3/application/...). Dieses zuätzliche Verzeichnis muss bei den Befehlen beachtet werden.

* Anpassung der Konfigurationsdatei parameters.yml
* Erzeugen der Datenbank
* Erzeugen des Datenbank Schemas
* Kopieren/Verlinken der Bundle' Assets in das öffentliche web-Verzeichnis
* Initialisierung des Rollen-Systems
* Erzeugen des "root"-Benutzers
* Einfügen  der Projektions-Definitionen
* Einfügen der Anwendungen aus der mapbender.yml in die Datenbank


Referenzieren Sie auf der Verzeichnis web über einen Symbolischen Link
[555555555555555555555555555555555555555555555555555555555555555555555]

Als Entwickler werden Sie es bevorzugen, über einen Symbolischen Link auf das Verzeichnis web zu verweisen statt die DAteien zu kopieren. 
Dies vereinfacht das Editieren von Assets innerhalb der Bundle-Verzeichnisse.

.. code-block:: yaml

    app/console assets:install web --symlink --relative


Bitte beachten Sie, dass Sie die Option :command:`FollowSymLinks` in der Apache Directory Definition angeben müssen:


.. code-block:: yaml

  Alias /mapbender3 /var/www/mapbender-starter/application/web/
  <Directory /var/www/mapbender-starter/application/web/>
    Options MultiViews FollowSymLinks
    DirectoryIndex app.php
    Order allow,deny
    Allow from all
    
    RewriteEngine On
    RewriteBase /mapbender3/
    RewriteCond %{ENV:REDIRECT_STATUS} ^$
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(.*)$ app.php/$1 [PT,L,QSA]
 </Directory>


Lernen Sie mehr über app/console
[5555555555555555555555555555555]
Die Symfony Console Komponenten ermöglichen es, kommandozeilen basierte Befehle zu erzeugen. Doctrine verfügt beispielsweise über einige kommandozeilen basierte Befehle, die Sie verwenden können.

Lesen Sie mehr in der Symfony Dokumentation über `Console Commands <http://symfony.com/doc/current/components/console/usage.html>`_.

Hier finden Sie einige Kommandos zum Auffinden von Informationen:

.. code-block:: yaml

 app/console                        - lists all assets
 app/console help                   - Anzeige der Hilfe
 app/console help list              - Anzeige der Hilfe für einzelne Kommandos
 app/console doctrine               - Anzeige aller Funktionen von Doctrine 
 app/console mapbender              - Anzeige aller Funktionen von Mapbender
 app/console help assets:install    - Anzeige der Hilfe zu speziellen Kommandos


Lernen Sie wie Sie eigene Elemente über *app/console mapbender:generate:element* erzeugen können `How to create your own Element? <../../../en/book/development/element_generate.html>`_.
        
..
 Package Build Tools
[6666666666666666666]

 TODO: Skipped for now, KMQ has the knowledge.

Aktualisierung der Installation
[666666666666666666666666666666]
Da die Entwicklungen voranschreiten, wollen Sie ihren Code aktuell halten. 

Folgende Schritte müssen durchgeführt werden:

* Holen Sie den Code vom mapbender-starter Repository
* Aktualisieren Sie die Submodule
* Aktualisieren Sie die Datenbank, um gegebenenfalls neue Strukturen (Tabellen, Spalten) zu erzeugen


.. code-block:: yaml
 
 cd mapbender-starter
 git pull
 git submodule update --init --recursive
 cd application
  ./composer.phar update --dev
 app/console doctrine:schema:update


.. _installation_sphinx:

Sphinx
[66666]

Sphinx wird für die Dokumentation benötigt, die Sie gerade lesen. In Debian-basierten Systemen wird Sphinx folgendermaßen installiert.


.. code-block:: yaml

   sudo apt-get install sphinx-common


Sie finden die Mapbender3 Dokumentation auf github unter  mapbender-documentation. Sie könnnen den Klon über den Befehl holen: 

.. code-block:: yaml

	git clone git://github.com/mapbender/mapbender-documentation

Entwickler mit Schreibrechten müssen die SSH-URL verwenden: git@github.com:mapbender/mapbender-documentation

Lesen Sie mehr über `How to write Mapbender3 Documentation? <../../../en/book/development/documentation_howto.html>`_.

ApiGen
[66666]

`ApiGen <http://apigen.org>`_ ist der API-Dokumentations-Generator erster Wahl. Es wird auch mit Pear installiert: 


.. code-block:: yaml
    
	 sudo pear install pear.apigen.org/apigen


Lesen Sie mehr in `How to write Mapbender3 Documentation? <../../../en/book/development/documentation_howto.html>`_.

Troubleshooting
[55555555555555]

* Die ApiGen-Bestandteile laufen nur mit neueren Versionen von Phing (>= 2.4.12). Testen Sie die Phing Version mit: 

.. code-block:: bash

              phing -v


Mit dem folgenden Befehl können Sie ein Update all Ihrer Pear-Pakete vornehmen: 


.. code-block:: bash

    sudo pear upgrade-all
      Enable full APC compatibility [yes] : yes
      Enable internal debugging in APCu [no] : yes
