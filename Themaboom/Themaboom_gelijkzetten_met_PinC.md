# Themaboom gelijkzetten met PinC [gepland]

## Inleiding

Wil je als centrumstad je themaboom gelijkzetten met de themaboom van PinC, dan zul je in de nabije toekomst hiervan gebruik kunnen maken. Je hoeft dit script niet zelf te runnen: het script kan op regelmatige basis gerund worden door PinC. Het script produceert een Excel-bestand, dat met de centrumsteden gedeeld kan worden via de connector. Wil je als centrumstad je themaboom gelijkzetten met PinC, dan kun je dat Excel-bestand importeren. Het bestand bevat een selectie van de externe themaboom van PinC, met alle thema’s, subthema’s en onderwerpen in dezelfde volgorde als op PinC. Maar het bestand bevat alleen de onderwerpen die vanuit PinC naar de centrumsteden doorstromen via de connector.

Let op: er zijn nog uitgebreidere testen nodig alvorens we dit kunnen gebruiken. Een eerste test heeft alvast uitgewezen dat het erg lang kan duren om een grote themaboom te importeren. We willen eerst weten of dit overal goed gaat.

Je moet er ook rekening mee houden dat elke Swing-implementatie zijn eigen limieten heeft voor wat betreft het aantal items in de themaboom. Als je een groot themaboom-bestand importeert, dan moet je eerst zeker zijn dat de limiet door de import niet bereikt of overschreden zal worden. In de Swing-omgeving van PinC kunnen we dit om die reden momenteel niet testen, want het themaboom-bestand dat we willen importeren, bevat veel meer items dan er in onze Swing-omgeving nog beschikbaar zijn.

## Werking van het script

Om het script te laten werken, moeten we eerst de externe themaboom van PinC exporteren. Dat gaat als volgt:

- log in bij Swing Studio
- klik op **Category tree**
- selecteer de map `Thema's` of `PRODUCTIE` om zowel de externe als de interne themaboom te exporteren
- klik op `EXPORT`

Er wordt nu een Excel-bestand gedownload met de naam `CategoryTree.xlsx`. Plaats dat bestand in dezelfde map als het script.

Daarna kan het script gerund worden. Het resultaat is een nieuw Excel-bestand met de naam `CategoryTree_import_PinC.xlsx`. Dat bestand kan (in theorie) in de Swing-omgevingen van de centrumsteden geïmporteerd worden.

Om dit voor elkaar te krijgen gaat het script als volgt te werk:

Het script maakt eerst een lijst van alle onderwerpen die in de connector zitten. (De connector-onderwerpen bevinden zich in de interne themaboom van PinC.) Alleen die onderwerpen komen in aanmerking om in het resulterende Excel-bestand opgenomen te worden.

Het script overloopt vervolgens alle items in de externe themaboom van PinC, in volgorde. Enkel de onderwerpen die ook in de connector zitten, worden behouden; al de rest wordt verwijderd.

Het resultaat is een subset van de externe themaboom van PinC, waarin alleen de connector-onderwerpen voorkomen.

Om dit te kunnen importeren bij de centrumsteden, moeten we wel nog de indicatorcodes wijzigen: alle codes die via de connector gaan, krijgen bij de centrumsteden immers het prefix `dna_`. Het script zal dus overal die prefix toevoegen, zodat de codes overeenstemmen met de codes in de databank van de Swing-omgeving van de centrumsteden.

## Import

Het is natuurlijk niet de bedoeling dat de (externe) themaboom van de centrumsteden zomaar wordt overschreven wanneer het bestand wordt geïmporteerd.

Daarom staan alle te importeren onderwerpen aanvankelijk onder een tijdelijke map, die je kunt hernoemen zoals je wilt.
