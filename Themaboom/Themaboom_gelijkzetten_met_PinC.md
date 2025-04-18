# Themaboom gelijkzetten met PinC [gepland]

## Inleiding

Wil je als centrumstad je themaboom gelijkzetten met de themaboom van PinC, dan zul je in de nabije toekomst hiervan gebruik kunnen maken. Je hoeft dit script niet zelf te runnen: het script wordt op regelmatige basis gerund door de beheerders van PinC. Het script produceert een Excel-bestand, dat met de centrumsteden gedeeld kan worden via de connector. Wil je als centrumstad je themaboom gelijkzetten met PinC, dan kun je dat Excel-bestand importeren. Het bestand bevat een selectie van de externe themaboom van PinC, met alle thema’s, subthema’s en onderwerpen in dezelfde volgorde als op PinC. Maar het bestand bevat alleen de onderwerpen die vanuit PinC naar de centrumsteden doorstromen via de connector.

Let op: er zijn nog uitgebreidere testen nodig alvorens we dit kunnen gebruiken. Een eerste test heeft alvast uitgewezen dat het erg lang kan duren om een grote themaboom te importeren. We willen eerst weten of dit overal goed gaat.

Je moet er ook rekening mee houden dat elke Swing-implementatie zijn eigen limieten heeft voor wat betreft het aantal items in de themaboom. Als je een groot themaboom-bestand importeert, dan moet je eerst zeker zijn dat de limiet door de import niet bereikt of overschreden zal worden. In de Swing-omgeving van PinC kunnen we dit om die reden momenteel niet testen, want het themaboom-bestand dat we willen importeren, bevat veel meer items dan er in onze Swing-omgeving nog beschikbaar zijn.

Je kunt de limieten die van toepassing zijn op jouw Swing-omgeving controleren door in te loggen in Swing Studio (de beheersomgeving van Swing) en vervolgens in het menu rechtsboven `Help` en vervolgens `About Studio` te kiezen.

![About Studio](images/swing_studio_menu_about.png)

Je krijgt dan een overzichtspagina te zien. Bij provincies.incijfers.be ziet die pagina er bijvoorbeeld als volgt uit (op 17 april 2025):

![About Studio](images/swing_studio_about.png)

Voor de themaboom is de limiet ‘maximum amount of category tree items’ van belang.

## Werking van het script

Om het script te laten werken, moeten we eerst de volledige (externe + interne) themaboom van PinC exporteren. Dat gaat als volgt:

- log in bij Swing Studio
- klik op **Category tree**
- selecteer de root (`Thema's`) of de map `PRODUCTIE` om zowel de externe als de interne themaboom te exporteren
- klik op `EXPORT`

Er wordt nu een Excel-bestand gedownload met de naam `CategoryTree.xlsx`. Plaats dat bestand in dezelfde map als het script.

Daarna kan het script gerund worden. Het resultaat is een nieuw Excel-bestand met de naam `CategoryTree_import_PinC.xlsx`. Dat bestand kan (in theorie) in de Swing-omgevingen van de centrumsteden geïmporteerd worden (zolang daarbij de limiet ‘maximum amount of category tree items’ niet overschreden dreigt te worden).

Om dit voor elkaar te krijgen gaat het script als volgt te werk:

Het script maakt eerst een lijst van alle onderwerpen die in de **connector** zitten. De connector-onderwerpen bevinden zich in de interne themaboom van PinC, onder Swing Connectoren > Uitgaande connectoren > Centumsteden > Swing Connector Centrumsteden. (Ja, we hebben het ook gemerkt: er ontbreekt een ‘r’ in ‘Centumsteden’...) Alleen die onderwerpen komen in aanmerking om in het resulterende Excel-bestand opgenomen te worden.

Het script overloopt vervolgens alle items in de **externe themaboom** van PinC, in volgorde. Enkel de onderwerpen die ook in de connector zitten, worden behouden; al de rest wordt verwijderd.

Het resultaat is een subset van de externe themaboom van PinC, waarin alleen de connector-onderwerpen voorkomen en waarbij de volgorde van de externe themaboom van PinC behouden blijft.

Om dit te kunnen importeren bij de centrumsteden, moeten we wel nog de indicatorcodes wijzigen: alle codes die via de uitgaande connector gaan, krijgen bij de centrumsteden immers het prefix `dna_`. Het script zal daarom overal die prefix toevoegen, zodat de codes overeenstemmen met de codes in de databank van de Swing-omgeving van de centrumsteden.

Momenteel (april 2025) worden er meer dan 10.630 items uit de externe themaboom van PinC (voornamelijk onderwerpen, maar ook enkele rapporten) gedeeld via de connector.

## Import

Het is natuurlijk niet de bedoeling dat de (externe) themaboom van de centrumsteden zomaar wordt overschreven wanneer het bestand wordt geïmporteerd.

> _De bestaande themaboom overschrijven met een nieuwe is overigens niet zomaar mogelijk: met een importbestand kunnen alleen maar nieuwe items toegevoegd worden en bestaande items aangepast worden, maar er kunnen met een import nooit bestaande items verwijderd of verplaatst worden._

Daarom staan alle te importeren onderwerpen aanvankelijk onder een tijdelijke map, die je kunt hernoemen of verplaatsen zoals je wilt. Die tijdelijke map heet `import_PinC`.

Om het Excel-bestand `CategoryTree_import_PinC.xlsx` te importeren, ga je als volgt te werk:

- log in bij Swing Studio
- klik op **Category tree**
- klik op `IMPORT` in het menu
- kies het bestand `CategoryTree_import_PinC.xlsx`
- klik op de groene `IMPORT`-knop

Het importeren van meer dan tienduizend themaboom-items kan erg lang duren. Blijf echter alert om te vermijden dat je automatisch uitgelogd wordt uit Studio terwijl het importproces nog bezig is. Na zowat 25 minuten kun je volgende boodschap op het scherm zien verschijnen:

![Time-out](images/swing_session_inactive.png)

Klik op `CONTINUE` om te vermijden dat je uitgelogd wordt.

Bij een test in de bèta-omgeving van PinC duurde het zowat een half uur om een bestand met 3.000 items te importeren. Vermoedelijk zal het importeren van een bestand met 10.000 items dus tussen anderhalf en twee uur duren (waarbij je meermaals bovenstaande boodschap kunt zien).

Wanneer de import klaar is, krijg je volgende melding te zien:

![Import result](images/import_category_tree_1.png)

Klik op `CLOSE` om dit venster te sluiten. Je vindt de nieuwe map `import_PinC` nu helemaal aan het einde van de themaboom.

De map zal vooralsnog enkel zichtbaar in de admin-omgeving, nog niet in de live versie. Dat gebeurt pas wanneer de databank opnieuw gepubliceerd wordt. Maar vóór dat gebeurt, wil je de map wellicht eerst hernoemen en/of verplaatsen.

### Themaboom aanpassen

Je kunt nu de themaboom aanpassen en inrichten zoals je zelf wilt en de zopas geïmporteerde map hernoemen en/of verplaatsen.

Heb je in je huidige externe themaboom geen eigen onderwerpen, rapporten, presentaties en URL-links, maar heb je uitsluitend items die uit PinC komen? Dan kun je je eigen externe themaboom volledig vervangen door de geïmporteerde PinC-themaboom.

Heb je echter niet alleen maar items staan die uit PinC komen, maar heb je ook nog eigen onderwerpen, rapporten, presentaties en URL-links? Dan wil je die natuurlijk behouden. Je kunt dan de geïmporteerde PinC-themaboom opnemen in een submap van je bestaande externe themaboom (en overbodige themaboom-items verwijderen).

Het spreekt vanzelf dat je hierbij de nodige voorzichtigheid aan de dag moet leggen. Een foutje is snel gemaakt, en je wilt natuurlijk niet dat je gebruikers hun vertrouwde thema’s en onderwerpen niet meer kunnen vinden.

Binnen Studio kun je in de themaboom mappen verplaatsen door ze te verslepen, maar we raden dit ten sterkste af omdat het op die manier al heel snel fout kan gaan. Als je een map wilt verplaatsen, dan ga je beter als volgt te werk:

- Klik op de map die je wilt verplaatsen (bijvoorbeeld de map `import PinC`). Daardoor wordt die map geselecteerd. Dat merk je doordat de achtergrond een andere kleur krijgt.
- Klik nu nogmaals met de rechtermuisknop en kies `Cut` in het contextmenu. Daardoor wordt de geselecteerde map naar het klembord gekopieerd.
- Klik vervolgens op een andere map (bijvoorbeeld de map `Extern`). Daardoor wordt de aangeklikte map geselecteerd.
- Klik nu nogmaals met de rechtermuisknop en kies `Paste` in het contextmenu. Daardoor wordt de inhoud van het klemboord verplaatst naar de geselecteerde map. Concreet wordt de map `import PinC` daardoor een submap van `Extern`.

Eenmaal de map verplaatst is, kun je de map hernoemen. Dat kan door de map te selecteren en vervolgens op functietoets `F2` te klikken. Je kunt de naam van de map nu wijzigen.

Om een overbodige map te verwijderen, ga je als volgt te werk:

- Klik met de rechtermuisknop op de map die je wilt verwijderen.
- Kies `Remove` in het contextmenu.

Je krijgt nu nog een dialoogvenster met een waarschuwing te zien, want deze actie kan niet ongedaan gemaakt worden. Klik op de rode `DELETE`-knop om de map (inclusief alle inhoud) definitief te verwijderen.

![Delete](images/swing_studio_category_tree_delete.png)
