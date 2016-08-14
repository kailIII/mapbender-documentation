.. _installation_symfony:

Installation im Symfony eigenen Webserver
[4444444444444444444444444444444444444444]

Mapbender3 baut auf dem `Symfony <http://symfony.com/>`_ Framework auf und kann daher den in `Symfony eingebauten Webserver <http://symfony.com/doc/current/cookbook/web_server/built_in.html>`_ nutzen. Das ermöglicht Ihnen einen schnellen Test von Mapbender3, ohne eine Integration in einen Webserver vorzunehmen. Dies eignet sich nicht für Produktivumgebungen. In dieser Anleitung wird die SQLite Datenbank verwendet. 

* Beachten Sie die `Systemvoraussetzungen <systemrequirements.html>`_
* Laden Sie Mapbender3 herunter.
* Entpacken Sie Mapbender3 in ein beliebiges Verzeichnis.
* Kopieren Sie sich die parameters.yml.dist nach parameters.yml

  .. code-block:: bash

                  cp app/config/parameters.yml.dist app/config/parameters.yml


* Starten sie den Symfony eigenen Webserver:

  .. code-block:: bash

                  app/console server:run

* Mapbender3 ist danach über die Adresse http://localhost:8000/app.php erreichbar.


In Virtuellen Umgebungen
[55555555555555555555555]

Falls Sie Mapbender3 in einer virtuellen Maschine laufen lassen wollen und über den Hostrechner darauf zugreifen möchten, geben Sie folgenden Befehl ein.

    
.. code-block:: bash

                app/console server:run 0.0.0.0:8000

Mapbender3 ist dann vom Host-Rechner aus über http://ip-adresse:8000/app.php erreichbar.
