# MediaWiki Guide

Wikis sind ein wichtes Mittel zur Generierung und Zugänglichmachung von Wissen.

Für Forschungsprojekte hat die Verwendung von Wikis eine Reihe bedeutender Vorteile:
* Sie sind kollaborativ. Es erlaubt den Forscherinnen ihr Wissen in einer zentralen Stelle zu sammeln.
* Sie sind nachvollziehbar. Da die Revisionsgeschichte der Dokumente einsehbar ist, ist die Arbeit mit Wikis grundsätzlich transparent.
* Sie sind leicht erlernbar. Da Mediawiki das System ist, das auch Wikipedia verwendet, haben inzwischen wahrscheinlich alle eine gewisse Vorerfahrung bzw. eine gewisse Intutition dafür, wie das System funktioniert.

## Das Ökosystem

### MediaWiki

Die Software, die auch für Wikipedia eingesetzt wird.

#### Installation

Für eine schnelle Installation mit Docker kann man folgendes Docker-Compose File verwenden: https://github.com/KompetenzwerkD/mediawiki-docker


#### Verwendung

##### Templates
##### Organisation

#### Strukturierte Daten?

MediaWikis erlauben es auf einfache Weise Wissen zu teilen. Dieses Wissen liegt in für Menschen leicht lesbare Form (Texte bzw. Mediendateien) vor. Im Gegensatz dazu sind sie aber nicht dafür ausgelegt, einzelne Fakten/Informationen maschniell abrufbar zu machen bzw. Fakten automatsiche zu aggregieren. 

Um dieses Defizit auszugleichen gibt es enige Erweiterungen zu MediaWiki, die es erlauben Daten strukturiert zu erfassen und abzufragen. Die beiden wichtigsten hierfür sind Wikibase und Sematic MediaWiki.

Es gibt auch Bemühungen Wikidata/Wikibase und Sematic MediaWiki näher zusammenzubringen. Z.B. https://professional.wiki/en/articles/semantic-wikibase


### Wikidata/Wikibase

Wikibase ist eine freie Erweiterung zu MediaWiki, welche mithilfe derer maschinlesbare, struturierte Wissensdatenbanken erstellt werden können. Es verwendet dabei LOD Prinzipien und die Daten können mittels SPARQL abgefragt werden bzw. u.a. als RDF/XML, N3, Json, Yaml etc. exportiert werden. 

[Das Wikibase Datenmodell](https://www.mediawiki.org/wiki/Wikibase/DataModel/Primer) ist sehr flexibel, und basier auf zwei Typen von Entitäten: Items und Properties. Zu jeder Entität können Fakten in form von Statements (semantsiche Tripel) angelegt werden. Diese Statements können weiter qualifiziert bzw. mit Referenzen versehen werden. 

Items und Properties werden mit mit numerischen IDs angelegt und mittels Labels bezeichnet. Dadurch ist Wikibase grundsätzlich auf mehrsprachigkeit ausgelegt.

```    
Item
        Item identifier (number prefixed with Q)
        Fingerprint, consisting of:
            Multilingual label*
            Multilingual description*
            Multilingual aliases
        Statements, each consisting of:
            Claim, consisting of:
                Property
                Value
                Qualifiers (additional property-value pairs)
            References (each consisting of one or more property-value pairs)
            Rank
        Site links
Property
        Property identifier (number prefixed with P)
        Fingerprint, consisting of:
            Multilingual label*
            Multilingual description*
            Multilingual aliases
        Statements, each consisting of:
            Claim, consisting of:
                Property
                Value
                Qualifiers (additional property-value pairs)
            References (each consisting of one or more property-value pairs)
            Rank
        Datatype
```

"Gerade das wikidata-Projekt könnte dabei in Zukunft eine besondere Rolle als Link-Hub für die Geisteswissenschaften spielen. Das dort gesammelte Wissen ist relativ stabil, die Adresse etabliert und es stehen kuratierte Daten zur Verfügung, die alle Bereiche menschlichen Erkenntnisinteresses abbilden. Wenn Semantic Web irgendwann funktionieren wird, dann werden Projekte wie dbpedia und neuerdings wikidata darin sicher weiterhin eine zentrale Rolle spielen."

Wettlaufer, Jörg (2018), "Der nächste Schritt? Semantic Web und digitale Editionen". In: Digitale Metamorphose: Digital Humanities und Editionswissenschaft. Hg. von Roland S. Kamzelak / Timo Steyer. (= Sonderband der Zeitschrift für digitale Geisteswissenschaften, 2). DOI: 10.17175/sb002_007 .

#### Installation

Der Wikimedia Deutschland e.V. stellt ein Docker-Compose File zur verfügung: https://github.com/wmde/wikibase-docker
Für den Betrieb einer Wikiase Instanz wird empfohlen mindesten 4GB Ram zur Verfügung zu stellen.

#### Verwendung

##### Quickstatements

##### Wikidata Query Service



### Semantic MediaWiki

Semantic MediaWiki (SMW) ist wie Wikibase eine freie Extension für MeidaWiki. SMW erlaubt es Informationen in Wikiseiten semantsich anzureichern, bzw. diese mit semantsichen Daten zu ergänzen. Dies erlaubt das im Wiki gesammelte Wissen auf neue Weise sortierbar und durchsuchbar zu machen. 

Einen Überblick von DH Projekten, die Sematic MediaWiki einsetzen findet man hier:
https://www.semantic-mediawiki.org/wiki/Projects_in_eHumanities_running_Semantic_MediaWiki

#### Verwendung

SMW erweitert Mediawiki um sogenante *properties* und *relations*. 

*Properties* erlauben es eine Ressource (eine Wikiseiten) strukturiert mit spezifischen Informationen zu versehen. Ein Property hat dabei einen bestimmten 'Datentyp' (Links). Die Properties werden als Trippel formuliert z.B. 

"Stefan Zweit" "Geboren am" "28.11.1881"

In der Wikiseite von "Stefan Zweig" würde die Information wie folgt eingetragen werden:

`Stefan Zweig wurde am [[Geboren am::28.11.1881]] in Wien geboren.`

*Relations* sind im SMW verbindungen zwischen zwei Ressourcen (Wikiseiten). Wie properties werden auch sie als semantsiche Tripel formuliert.
 
`"Seite A" "steht in Verbindung zu" "Seite B"`

z.B.

`"Die Welt von Gestern" "hat Autor" "Stefan Zweig"

In der WikiSeite von "Die Welt von Gestern" würde diese Information folgenderweise eingechreiben werden:

`"Die Welt von Gester [...] ist ein autogiographisches Werk von [[hat Autor::Stefan Zweig]]."`

Im diesen Sinne wird eine *relation* wie eine *property* mit dem Datentyp "page" verwendet. 


### Weitere nützliche MediaWiki Extensions

#### Cite

[Website](https://www.mediawiki.org/wiki/Extension:Cite/de)
[Anwendung](https://www.mediawiki.org/wiki/Help:Cite/de)


Erlaubt die Verwendung von Referenzen und Fußnoten mittels 

`<ref>` 
und
`<references />`

Diese Erweiterung ist standardmäßig im Mediawiki enthalten muss aber eventuell über in der `LocalSettings.php` eingetragen werden:

`wfLoadExtension( 'Cite' );`


#### Graph

[Website](https://www.mediawiki.org/wiki/Extension:Graph)
[Andwendung](https://www.mediawiki.org/wiki/Extension:Graph/Guide)

Mit der Graph Erweiterung können mittels den `<graph> ... </graph> Tags Visualisierungen (Charts, Timelines, Histogramme)` in Wikiseiten eingebunden werden.

Um Graph verwenden zu können, muss auch die [JsonConfig](https://www.mediawiki.org/wiki/Extension:JsonConfig) Erweiterung installiert werden.

Es existieren in Wikipedia eine Reihe praktischer Templates für Graph-Charts:
* [Template:Graph:Chart](https://en.wikipedia.org/wiki/Template:Graph:Chart)

TODO: Importmöglichkeit der Wikipedia Graph Templates in Mediawiki ausprobieren!


#### Maps

[Website](https://www.mediawiki.org/wiki/Extension:Maps/de)
[Anwendung](https://www.semantic-mediawiki.org/wiki/Extension:Maps)

MediaWiki Erweiterung zur Einbindung von Karten.


## Nützliche Links:

* https://guides.library.ucla.edu/semantic-web/wikidata
