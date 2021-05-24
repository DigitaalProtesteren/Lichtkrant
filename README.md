# Lichtkrant

Een lichtkrant als protestbord of voor op een hoed.

## Benodigde materialen & gereedschap

* Arduino micro of Arduino nano (makkelijk aan te sluiten vanwege de USB connector) optioneel kan een andere Arduino ook of een ESP8266 of ESP32 maar dan moet je meer solderen.
* (Optioneel) Elektrolytische condensator van 470 uF of meer (10V of meer)
* 8 x 32 pixel flexibel ws2812 matrix
  Verkrijgbaar bij o.a. de volgende webshops:
  * https://nl.aliexpress.com/item/33025679652.html
  * https://www.hobbyelectronica.nl/product/8x32-rgb-ws2812b-led-flex-module/?gclid=EAIaIQobChMI5fu85tn_7wIVhaZ3Ch3kEw4IEAQYAiABEgJ_G_D_BwE
  * https://nl.grandado.com/products/ws2812b-led-digitale-flexibele-dc5v-individueel-adresseerbare-panel-licht-ws2812-8x8-16x16-8x32-module-matrix-scherm?variant=32322300903477
  * https://www.amazon.nl/dp/B07KT1H481
  * https://www.tinytronics.nl/shop/nl/diversen/led-matrix/ws2812b-digitale-5050-rgb-led-matrix-32x8-flexibel
* Powerbank met USB aansluiting
* USB kabel die past op de Arduino micro of nano

* Soldeergereedschap (soldeerbout met medium of kleine punt en soldeer)
* ducttape
* dun draad met vaste kern of een stukje (dun) touw

## Instructies

Desoldeer de aansluiting voor data output (de mannelijke connector) van het scherm maar bewaar de connector, die wordt in de volgende stap hergebruikt.
![Aansluitingen scherm](/MatrixAansluiting.jpg)

Soldeer de net verkregen connector aan de Arduino:
* Rode draad op de 5V aansluiting.
* Zwarte of witte draad op GND.
* Groene draad op pin 6 (bij een ESP8266 of ESP32 sluit je de groene draad aan op pin 13 - D3).

Soldeer eventueel de elektrolytische condensator op de losse rode en witte of rode en zwarte draad die van het scherm afkomt (in de afbeelding "Increase Voltage Wire genoemd). 

LET OP, de condensator heeft een witte streep of aanduiding die de negatieve kant aangeeft. Deze dient op de witte of zwarte draad aangesloten te worden, de andere kant van de condensator is voor de rode draad. Controleer of je de polariteit goed hebt aangesloten en isoleer de aansluitingen met ducttape.

Sluit de Arduino aan op de computer en upload de sketch (hoedtekst.ino).

Zet het scherm vast op een bord of om een (hoge)hoed heen. Bij een hoge hoed kan je de krant op de rand laten rusten en met een draad tussen de LEDs door om de hoed heen vastbinden.

## Aanpassen van de teksten
Je kan de teksten in de sketch makkelijk aanpassen. Vanaf regel 62 staan vier teksten die afgebeeld worden, hier kan je makkelijk nieuwe teksten toevoegen of weghalen:

    String mytext[] = 
      { 
        "Wie vrijheid inruilt voor veiligheid verdient geen van beiden", 
        "Wie vrijheid inruilt voor veiligheid verdient geen van beiden", 
        "Wie vrijheid inruilt voor veiligheid verdient geen van beiden", 
        "Wie vrijheid inruilt voor veiligheid verdient geen van beiden", 
     };

Naast de tekst heeft de sketch nog 2 onderdelen nodig. Als je teksten toevoegt moet je ook extra 0-en toevoegen in regel 59:

    int textlen[] = { 0, 0, 0, 0 };

En je moet meegeven bij regel 45 welke kleur je de tekst wil hebben, dat kan per tekst verschillen, in dit voorbeeld is dat Oranje, Rood, Wit en Cyaan. Voeg kleuren toe als RGB waarde, waarbij het eerste getal de hoeveelheid Rood is, het tweede getal hoeveel Groen en het derde getal hoeveel Blauw:

    const uint16_t colors[] = {
        matrix.Color(255,165,0), matrix.Color(255, 0, 0), matrix.Color(255, 255, 255), matrix.Color(0, 255, 255)
    };

Het aantal getallen bij regel 59 en het aantal matrix.Color(x, x, x) definities in regel 45 moeten overeenkomen met het aantal teksten.
