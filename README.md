# connectorbeheer

Gebruik de Issues hier indien je problemen hebt met data die je ontvangt via de Swing Connector.

## Basisprincipes

Via de Swing Connector kan je een pakket data ontvangen vanuit provincies.incijfers.be. Dit omvat alle instellingen en metadata van het onderwerp, inclusief privacy-maatregelen. Dit pakket is samen met de Centrumsteden ontwikkkeld, via de werkgroep OBMI van het Kenniscentrum Vlaamse Steden. Het gaat hier doorgaans over werk dat de provincies sowieso gingen doen, maar dat eventueel uitgebreid of versneld aangepakt wordt op basis van de vragen van de Centrumsteden. Daarnaast voegen de databeheerders van provincies.incijfers.be ook spontaan data toe als deze extern gepubliceerd wordt door hen. Alle data die extern beschikbaar is, kan sowieso hergebruikt worden. Dat doet ook ABF in zijn product gemeente.incijfers.be , waar gemeenten een volledig beheerde en opgevulde Swing versie kunnen kopen.

Het pakket data waar het om gaat kan je raadplegen in [de Excel die je in *provinciesincijfers/connectorbeheer* vindt](https://github.com/provinciesincijfers/connectorbeheer/blob/master/00_swing_connector_overzicht.xlsx) , of na inloggen op provincies.incijfers.be/databank in de map INTERN/Swing Connectoren/Uitgaande connectoren/Centrumsteden. Een kopie van deze mappenstructuur wordt ook overgezet naar de Swing van de klant.

Om zeker te zijn dat eigen data van de klant niet overschreven wordt, worden alle interne codes voorafgegaan door "dna_". 

Je kan binnen een klant-versie dus eenvoudig zoeken op deze code om lijsten te trekken van wat je via de Connector krijgt. Je kan ook filteren op "Beschermd", aangezien al onze dat beveiligd worden tegen mogelijk privacy-gevoelige bewerkingen.

Data kan door de Connector niet automatisch gewist worden. Dat zou ook geen goed idee zijn. Zie de uitleg over het [laten uitdoven van data](https://github.com/provinciesincijfers/JiveDocumentation/blob/master/levensloop_onderwerpen.md) voor meer uitleg en praktische tips.

Meer technische details over het opzet en de privacy-maatregelen [vind je hier](https://share.vlaamsbrabant.be/share/s/jb0ZsN95Ry-8FVSRA3DMnw).

## Updates

De updates lopen wekelijks tijdens het weekend op basis van de gepubliceerde databank van provincies.incijfers.be. Indien er geen nieuwe provincies.incijfers.be versie is gepubliceerd, gebeurt er niets. Tijdens dit proces worden enkel bestaande reeksen vernieuwd, inclusief metadata. 
Uitbreidingen worden op voorhand aangekondigd, met een frequentie van om de één a twee maand.
