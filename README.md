# connectorbeheer

Deze repository wordt in de eerste plaats gebruikt voor het beheer van de Swing Connector provincies.incijfers.be -> centrumsteden.
Fouten in dit proces kunnen gemeld worden via [de Issues hier](https://github.com/provinciesincijfers/connectorbeheer/issues).
Hieronder een uitleg over wat de Connector juist is, met vervolgens de praktische implementatie voor de Centrumsteden toegelicht.

## Wat is de Swing Connector

De Swing Connector (swg2swg) maakt het mogelijk om vlot data door te sturen van de ene Swing versie ("Donor") naar de andere ("Ontvanger"). Swing is de software die door ABF.nl geleverd wordt. Zij staan ook in voor het draaiend houden van het Connector-proces. 
Het gaat hier over Indicators (zowel platte onderwerpen als kubussen), inclusief de eigenschappen van de Indicator, de bijhorende drempel- en aggregatieonderwerpen, de kubusdimensies en de metadata. Dit omvat alle instellingen en metadata van het onderwerp, inclusief privacy-maatregelen.

## Technische aspecten

Bij de overdracht worden volgende veiligheidsmaatregelen genomen:
-	De Ontvanger kan drempelwaarde en afronding niet wijzigen (op de Indicator) of omzeilen (via een formule-onderwerp)
-	De Ontvanger kan de data niet exporteren via de Swing Studio
-	De Ontvanger kan wel formule-onderwerpen maken op de overgezette data, maar hierbij zal steeds het resultaat gecensureerd worden als er een gecensureerde waarde was in de data van de Donor

Data kan in Swing afgeschermd worden met Access Groups. Standaard wordt informatie over deze Access Groups niet overgezet. Als data dus niet gepubliceerd mag worden onder de vorm zoals die doorgegeven wordt, moeten hier afzonderlijke afspraken over gemaakt worden.
Tijdens het Connector proces worden alle gebiedsniveaus van de Ontvanger gevoed met correct geaggregeerde data.
Tijdens het Connector proces worden ook de benodigde extra onderwerpen zoals aggregatie- en drempelonderwerpen mee overgezet, zelfs als die niet expliciet in de Connector-map in de CategoryTree worden gedefinieerd.
De Indicators die via de Connector doorgestuurd worden, staan bij de Ontvanger aangeduid als “Beschermd onderwerp”. Dit is niet uit te zetten en beperkt de handelingen die de ontvangde beheerder met het onderwerp kan doen.


## Beheer in de praktijk

* De Donor voegt Indicators (platte onderwerpen en kubussen) toe aan een speciale map in de Category Tree. Deze map verschijnt ook in de interne CategoryTree van de Ontvanger.
* De Donor, Ontvanger en ABF maken samen afspraken over update-frequentie en details van de processen. De Connector loopt standaard op de gepubliceerde Donor databank en voedt de beheersomgeving van de Ontvangende databank. De Ontvanger moet dus zijn Swing Studio databank publiceren (live zetten) alvorens nieuwe cijfers zichtbaar worden voor eindgebruikers. 
* Het proces zet enkel over wat gewijzigd werd. Indien er geen nieuwe versie van de Donor-databank werd gepubliceerd, dan gebeurt er niets. Voor Indicators waar niets  wijzigde (data noch metadata), gebeurt er niets. Tijdens het Connector proces worden enkel gewijzigde reeksen vernieuwd, inclusief metadata.
* Elke keer dat het proces loopt, kunnen ook de beschrijvende velden van de Indicatoren mee overschreven worden. Dit wordt onderling afgesproken tussen de drie partners.
* Nieuwe jaargangen worden automatisch overgezet. Standaard wordt géén rekening gehouden met toegangsgroepen. 
* Nieuwe kubussen worden automatisch overgezet. Indien een kubusmodel werd gewijzigd, moet dit manueel aangepast worden door de Donor of ABF, vooraleer het proces kan lopen.
* Het is via de Connector niet mogelijk om data geautomatiseerd te **wissen** bij de Ontvanger. Het is wél mogelijk om data te overschrijven. De Donor kan dus in geval van nood eerder verstuurde data vervangen door ontbrekende waarden. Waar provincies.incijfers.be de donor is, volgt zij daarom deze procedure voor data die verouderd is geraakt: https://github.com/provinciesincijfers/JiveDocumentation/blob/master/01.%20Algemeen%20databeheer/Levensloop%20onderwerpen.md . Deze methode maakt ook de eigen interne werking efficiënter.
* Doorgaans worden Indicators die door de Connector stromen voorzien van een prefix. Bijvoorbeeld wordt Indicatorcode bij de Donor *v1234_omschrijving* indicatorcode *dna_v1234_omschrijving*. Op die manier kan eenvoudig uitgesloten worden dat een eigen Indicator van de Ontvanger overschreven wordt door een indicator van de Donor. Je kan binnen een klant-versie dus eenvoudig zoeken op deze code om lijsten te trekken van wat je via de Connector krijgt. De Ontvanger kan ook data die ze via Connectors krijgt detecteren door te filteren op "Protected".
* De Connector kan maar data doorgeven voor zover deze voor dezelfde gebiedsindelingen beschikbaar zijn in de twee betrokken Swing versies. Indien gebiedsniveaucode (vb. *statsec*) en gebiedscode (vb. *11002A00-*) identiek zijn, dan is er geen enkel probleem. De meeste data kan vervolgens binnen de Swing omgeving van de Ontvanger berekend worden. Als de data op meerdere gebiedsniveaus moet ingelezen worden (bijvoorbeeld voor medianen), dan moet deze afstemming van codes op meerdere gebiedsniveaus gebeuren. Wanneer het niet mogelijk is om de codes rechtstreeks af te stemmen, dan kan er eventueel gewerkt worden met een tussenliggende gebiedsaggregatie. Bijvoorbeeld als de Donor het gebiedsniveau *statistischesect* wil blijven noemen en de Ontvanger *statsec* wil blijven gebruiken, wordt er een onzichtbaar gebiedsniveau "statsec" aangemaakt binnen de Swing van de Donor. Dit heeft wel het nadeel dat het voor niet-aggregeerbare Indicators niet werkt. Hier is een arbeidsintensieve omweg voor, maar deze wordt best vermeden.

## Swing Connector provincies.incijfers.be -> Centrumsteden .incijfers.be

Via de Swing Connector krijgen de centrumsteden wekelijks bijgewerkte data vanuit provincies.incijfers.be . Dit pakket is samen met de Centrumsteden ontwikkeld, via de werkgroep OBMI van het Kenniscentrum Vlaamse Steden. Het gaat hier doorgaans over werk dat de provincies sowieso gingen doen, maar dat eventueel uitgebreid of versneld aangepakt wordt op basis van de vragen van de Centrumsteden. Daarnaast voegen de databeheerders van provincies.incijfers.be ook spontaan data toe als deze publiek gepubliceerd wordt door hen. 

Het pakket data waar het om gaat kan je raadplegen in [de Excel die je in *provinciesincijfers/connectorbeheer* vindt](https://github.com/provinciesincijfers/connectorbeheer/blob/master/00_swing_connector_overzicht.xlsx) , of na inloggen op provincies.incijfers.be/databank in de map INTERN/Swing Connectoren/Uitgaande connectoren/Centrumsteden. Een kopie van deze mappenstructuur wordt ook overgezet naar de Swing van de klant.

We gebruiken "dna_" als voorvoegsel voor codes van Indicators.

Het is de verantwoordelijkheid van de Centrumstad om Uitdovende gegevens te verwijderen uit de voor eindgebruikers zichtbare omgeving.


## Updates

De updates lopen wekelijks tijdens het weekend op basis van de gepubliceerde databank van provincies.incijfers.be. Indien er geen nieuwe provincies.incijfers.be versie is gepubliceerd, gebeurt er niets. Tijdens dit proces worden enkel bestaande reeksen vernieuwd, inclusief metadata. 
Uitbreidingen worden op voorhand aangekondigd, met een frequentie van om de één a twee maand.
