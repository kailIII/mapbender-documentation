.. _coordinates_display:

Coordinates Display (Koordinatenanzeige)
[555555555555555555555555555555555555555]

Das Koordinatenanzeige-Element zeigt die aktuelle Mausposition in den Kartenkoordinaten. Die Koordinaten sind abhängig vom eingestellten räumlichen Referenzsystem, welches im `Spatial Reference System Selector <../elements/srs_selector.html>`_ geändert werden kann.

.. image:: ../../../../../figures/coordinates_display.png
     :scale: 90

Konfiguration
[666666666666]

.. image:: ../../../../../figures/de/coordinates_display_configuration.png
     :scale: 80

* **Beschriftung anzeigen (Show title label):** Schaltet die Beschriftung an/aus. Die Beschriftung richtet sich nach dem Title.
* **Title:** Titel des Elements. Dieser wird in der Layouts Liste angezeigt. Der Titel wird angezeigt, wenn "Beschriftung anzeigen" aktiviert ist.
* **Tooltip:** Text, der angezeigt wird, wenn der Mauszeiger eine längere Zeit über dem Element verweilt.
* **Anchor:** Verankerung des Elements (left-top, left-bottom, right-top, right-bottom). Bestimmt die Position des Elements im Layout. 
* **Numdigits:** Anzahl der Nachkommastellen der Koordinaten.
* **Target:** ID des Kartenelements, auf das sich das Element bezieht.
* **Emtpy:** Angezeigter Text, wenn sich die Maus nicht in der Karte befindet (Standard: 'x= - y= -').
* **Prefix:** Präfix vor der X-Koordinate (Standard 'x= ').
* **Separator:** Separator nach X- und vor Y-Koordinate (Standard ' y= ').

YAML-Definition:
[777777777777777]

.. code-block:: yaml

   tooltip: 'coordinates display' # Text des Tooltips
   numDigits: 2                   # die Anzahl der Nachkommastellen, die jede Koordinate haben soll
   target: ~                      # ID des Kartenelements
   label: true                    # false/true, um den Button zu beschriften. Der Standardwert ist true.
   empty: 'x= - y= -'             # zeigt diesen Text, wenn die Maus sich nicht in der Karte befindet.
   prefix: 'x= '                  # zeigt ein Präfix vor der X-Koordinate
   separator: ' y= '              # zeigt einen Separator vor der Y-Koordinate


CSS-Styling
[6666666666]

Das Element kann über den folgenden CSS-Style angepasst werden, beispielsweise um die Breite zu vergrößern.

.. code-block:: css
                
                .mb-element-coordsdisplay { 
                    width: 500px; 
                }


Class, Widget & Style
[66666666666666666666]

* **Class:** Mapbender\\CoreBundle\\Element\\CoordinatesDisplay
* **Widget:** mapbender.element.coordinatesdisplay.js
* **Style:** mapbender.elements.css

HTTP Callbacks
[6666666666666]

Keine.

JavaScript API
[6666666666666]

reset
[7777]

<>

showHidde
[777777777]

<>

JavaScript Signals
[66666666666666666]

Keine.
