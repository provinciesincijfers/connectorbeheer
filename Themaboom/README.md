# Themaboom

## Inleiding: Swing

De vijf Vlaamse provincies en heel wat steden en gemeenten hebben hun eigen Swing-omgeving, met een eigen website en databank. Ze hebben allemaal één ding gemeen: er wordt gewerkt met de Swing-software van het Nederlandse bedrijf ABF Research (https://abfresearch.nl). De websites en de databanken van de provincies, steden en gemeenten worden gehost bij ABF. Voor Vlaanderen heeft ABF het internetdomein **[incijfers.be](https://incijfers.be/)** aangekocht. De provincies, steden en gemeenten die klant zijn bij ABF kregen daar een eigen subdomein, bv. **[provincies.incijfers.be](https://provincies.incijfers.be/)** (de vijf Vlaamse provincies), **[limburg.incijfers.be](https://limburg.incijfers.be/)** (de provincie Limburg) of **[kortrijk.incijfers.be](https://kortrijk.incijfers.be/)** (de stad Kortrijk). Het is ook mogelijk dat jouw gemeente of stad een eigen internetdomein heeft dat naar de Swing-website leidt, bv. [gent.buurtmonitor.be](https://gent.buurtmonitor.be).

Als je al die verschillende Swing-implementaties bekijkt, zul je heel wat gelijkenissen zien, maar ook enkele verschillen. Elke site kan namelijk op maat aangepast worden.

## Python-scripts

Er werden twee Python-scripts ontwikkeld met betrekking tot de themaboom. De scripts houden rekening met de verschillen tussen de verschillende Swing-omgevingen.

Een eerste script (`swing_category_tree.py`) reproduceert de volledige uitgeklapte themaboom, met een overzicht van alle thema’s, subthema’s en onderwerpen. Dit is handig om een volledig overzicht te hebben (én te doorzoeken) en om dit te delen met geïnteresseerde gebruikers.

Het tweede script (`pinc_category_import.py`) biedt steden en gemeenten een mogelijkheid (maar zeker geen verplichting) om hun themaboom gelijk te zetten met PinC voor wat betreft de onderwerpen die gedeeld worden via de connector.

## `swing_category_tree.py`

Dit script produceert één of meer HTML-bestanden met een overzicht van de volledige themaboom, met alle thema’s, subthema’s en onderwerpen als aanklikbare links die je direct naar de databank brengen.

Alvorens het script te runnen, moet er wel wat voorbereidend werk gebeuren: je moet minstens de themaboom en de onderwerpenlijst vanuit Swing Studio exporteren naar een Excel-bestand. Het script heeft die Excel-bestanden nodig om de themaboom te kunnen reproduceren.

Alle uitleg vind je onder [Uitgeklapte themaboom](Uitgeklapte_themaboom.md).

## `pinc_category_import.py`

Een aantal centrumsteden hebben de wens geüit om hun eigen themaboom gelijk te zetten met de themaboom van PinC, althans voor wat betreft alle onderwerpen die via de connector vanuit PinC doorstromen naar de Swing-implementaties van de steden.

Dit Python-script biedt daarbij een grote hulp. Het script produceert een Excel-bestand met een gedeeltelijke themaboom, die de centrumsteden in hun eigen Swing-omgeving kunnen importeren. Het bestand bevat alle thema’s, subthema’s en onderwerpen die gedeeld worden via de connector, in de volgorde waarin ze opgenomen zijn in de externe themaboom van PinC.
