# Connectorbeheer: How to connect

De databeheerders van provincies.incijfers.be gebruiken volgend stappenplan om de Connector voor de Centrumsteden periodiek aan te vullen.

## Stappenplan 

**Stap 0**: Zet een notitieblokje klaar waar je noemenswaardige zaken oplijst voor het info-tabblad van het Connectordocument, of om op de OBMI te vermelden.

**Stap 1**: Kijk in het [logboek](https://provincies.incijfers.be/admin/jive/Report/Edit/logboek) op PinC Dit geeft een indicatie van nieuwe datareeksen, actualisaties en wijzigingen sinds de laatste update.

:grey_exclamation: Opgelet: Het kan zijn dat het logboek niet volledig is. Ook niet alles is relevant voor gebruikers van de connector, enkel zaken die extern staan.

**Stap 2**: Maak een export van de **externe themaboom**. Verwijder in deze excel eerst de 2e, 3e en 4e kolom. Voeg vervolgens nog de kolommen 'staat in vorige connector?' toe en 'nieuw'. In stappen 4 en 5 zullen we deze kolommen invullen.

**ZijStap 2 bis**: We gebruiken de export van de **externe themaboom** die we net gemaakt hebben om de [toegang](https://github.com/provinciesincijfers/JiveDocumentation/blob/master/05.%20Themaboom%20-%20Toegang%20beheren/Toegangs-%20en%20gebruikersgroepen.md#themaboom-en-toegangsgroepen) tot [de odata service](https://provincies.incijfers.be/databank/report/?id=achter_de_schermen) bij te werken. Bewaar hiertoe enkel de Indicator codes met als kolomhoofd *Code*. Zet deze info in een Excelbestand met slechts één tabblad met data (anders faalt de import zonder foutmelding)/ Ga vervolgens naar [Accounts > Access groups > rij open_data > lijst INDICATORS](https://provincies.incijfers.be/admin/studio/Table/DetailItemGrid?TableName=AccessGroupItem&ParentKey=AccessGroupCode&ParentCode=9&ParentTable=AccessGroup&ItemKey=V). Gebruik "IMPORT METADATA" om de onderwerpen die hier staan uit te breiden.

**Stap 3**: Zorg ervoor dat je de laatste versie van Github > Provinciesincijfers > connectorbeheer hebt binnen getrokken op je lokale schijf, en open de excel [00_swing_connector_overzicht](https://github.com/provinciesincijfers/connectorbeheer/blob/master/00_swing_connector_overzicht.xlsx). Ga naar de tab 'draaitabel_onderwerpen', filter op de laatste release en kopieer dit naar de excel van de vorige stap, in een nieuwe tab.

**Stap 4**: In de kolom 'staat in vorige connector?' zoek je verticaal binnen de andere tab of de itemcode van de export van je themaboom, ook al voorkwam binnen de vorige release. Dit geeft dan bv de functie: =VERT.ZOEKEN(A2;Blad1!$A:$A;1;ONWAAR) waarin in Blad1 de kopie van de draaitabel staat.

**Stap 5**: Filter vervolgens op #N/B en bekijk welke zaken er 'echt' nieuw zijn en die in de connector moeten komen. Die geef je een '1' in de laatste kolom ('nieuw'). Als je zaken nog moet nakijken, plaats je hier 'nakijken'.

Belangrijk hierbij:

- Enkel indicatoren komen in de connector. Rapporten e.d. mag je dus negeren. (Nieuwe rapporten wel vermelden op de OBMI)
- Stroomvariabelen (vsxxxx) voegen we niet toe want deze gaan van gemeente x naar gemeente y. Enkel wanneer het subgemeentelijk is, kan het interessant zijn.
- Het kan zijn dat sommige indicatoren er 2x instaan, bv deze van levensverwachting.
- Cnt_xy_laadpalen moet niet in de connector.
- Sommige kubussen van Vicky mogen er niet in (kubus1403_ap en kubus1204_eff). Aangepaste kubussen voor de centrumsteden zitten al in de connector.
- De reeks 9101 (mobiliteit/enquete): want de Centrumsteden doen zélf de Stads- en Gemeentemonitor

Idealiter zie je hier het logboek in weerspiegeld, toch wat betreft NIEUWE thema's.

Wanneer er iets veranderd is waar je het niet verwacht (staat bv. niet in logboek), dan zoek je de nieuwe indicator op in de indicatorentabel en bekijk je hem. Wanneer er 1 indicator (en dus niet een hele reeks) naar boven komt, kan het zijn dat deze indicator per ongeluk gedelete was uit de Indicators tabel en daarom verdween op alle plaatsen in de themaboom, dus ook in de connector. Een verdwenen indicator die nadien terug werd toegevoegd, moet daarom terug toegevoegd worden aan alle mappen waar deze in zat. Vaak wordt de connector vergeten, dus dan lijkt het alsof deze nog niet in de connector zat, terwijl hij wel al bij de centrumsteden in de themaboom staan. Hierdoor kan deze niet meer geactualiseerd worden of op uitdovend worden gezet. Je moet deze dus terug in de connector steken zodat er terug een link is tussen onze data en de data die centrumsteden hebben. Waar een indicator allemaal staat, kan je enkel zien in de metadata van deze indicator. Je moet dit dan niet extra vermelden op de OBMI, maar gewoon terug in de connector steken.

**Stap 6**: Voeg de nieuwe variabelen toe aan de connector. Dit zijn alle variabelen waar een '1' naast staat in de kolom 'nieuw'

Er zijn drie scenario's:

(1) Nieuw thema: je kan de map gewoon kopiëren.

(2) Enkele nieuwe onderwerpen: manueel overzetten in de mappen.

(3) Als een thema werd geherorganiseerd, kan je alles uit de connector deleten en de nieuwe structuur overzetten. Dit is echter niet zonder gevaar! Zo kan je bv. dakloze onderwerpen krijgen. Uitdovende onderwerpen staan op deze manier niet meer in de connector, zodat het voor de centrumsteden niet duidelijk is welke onderwerpen uitdovend zijn en dus verwijderd moeten worden. Hierdoor is de beste oplossing om de oude indicatoren erin te laten staan, en dan de nieuwe in een nieuw mapje te steken zodat het voor hen duidelijk is.

:grey_exclamation: Vergeet niet waar nodig de relevante indicatoren in de map 'Beschikbaar op statsec' te plaatsen. Dit heeft technisch gezien geen enkel effect, maar is voor het gemak van de gebruiker.

:grey_exclamation: Zwier niet zomaar iets uit de connector, ALTIJD op uitdovend zetten.

:grey_exclamation: De connector map moet je updaten en publiceren vòòr het weekend voor de eerste OBMI.

**Stap 7**: Vul de excel aan [00_swing_connector_overzicht](https://github.com/provinciesincijfers/connectorbeheer/blob/master/00_swing_connector_overzicht.xlsx). De instructies staan in deze excel. Dit is het communicatie instrument naar de centrumsteden over wat er in de nieuwe release zit.

Belangrijk:

- In de tab **'voorbereiding'** plak je alles in de witte ruimte, waarbij je ervoor zorgt dat je niet per ongeluk in de grijze ruimte komt. Zorg dus voor genoeg plaats.
- Kopieer het lichtgrijze naar een nieuwe tab met de nieuwe releasedatum. Zo heb je het overzicht van de hele connector op dat moment.
- In de tab **'verzamel'** staat elke versie van elke connector onder elkaar, inclusief datum. Copy paste dus de tab van de nieuwe release, plak deze onderdaan en vul de datum aan.
- In de tab **'draaitabel'** (obv 'verzamel') kan je dan het aantal nieuwe onderwerpen zien en een leuke figuur. Voeg hiervoor nog de som toe van het aantal nieuwe onderwerpen. (dit laatste na volgende stap)
- Filter in de draaitabel vervolgens op de laatste en voorlaatste release, en kopieer vervolgens bij 'nieuwe onderwerpen' de nieuwe onderwerpen.
- Vul in de tab **'uitdovend'** de uitdovende en uitgedoofde onderwerpen aan.
- Voeg op de eerste tab '**info en handleiding'** een korte beschrijving toe van de release.
- Maak de tab met de derde laatste datum onzichtbaar.

**Stap 8**: 
- Push de excel naar github
- stuur Joris een mail met een korte beschrijving van de update. Dit is niet enkel de nieuwe / geactualiseerde data, maar bv ook een nieuw rapport of andere nieuwigheden. Dit kan ook voor de publicatie van de databank.
- Laat aan Richard weten dat de Connector-themaboom is bijgewerkt. Voorlopig wordt de themaboom niet meer automatisch gesynchroniseerd bij de wekelijkse update wegens een hardnekkige bug. Aangezien de inhoud van de themaboom niet vaak verandert, moeten we nu dus Richard op de hoogte brengen wanneer we de themaboom wijzigen.

Zorg ervoor dat je **ten laatste de vrijdag voor de OBMI publiceert**. 

## Overige belangrijke zaken

Check zeker ook Interne omgeving > swing connectoren > uitgaande > centrumsteden > geplande uitbreiding. Belangrijke veranderingen worden in deze map geplaatst. Dus als er bv iets aankomt, maar nog niet rijp is om gepubliceerd te worden, kunnen de centrumsteden dit al eens verkennen zonder dat het impact heeft op hun eigen omgeving. Zij kunnen dit enkel zien wanneer ze inloggen.
