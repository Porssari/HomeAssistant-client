# HomeAssistant-client
Pörssäri on mahdollista ottaa käyttöön myös Home Assistantin kautta. Home Assistant -laitteeseen lisätään automaattisesti 8 ohjauskanavaa. NordPoolin käyttöehtojen vuoksi käyttäjäkohtaista hintadataa ei ole pakettiin saatavilla.

Testattu toimivaksi HAOS versio 10.2 ja HA Core 2023.5 sekä 2023.6. Toimivuutta vanhemmilla versioilla ei ole varmistettu.

### Käyttöönotto
Lisää porssari_core.yaml -tiedosto Home Assistantin config-hakemistoon

Lisää seuraavat rivit configuration.yaml -tiedostoon:

```yaml
homeassistant:  
  packages:    
    porssari_core: !include porssari_core.yaml
```

Pörssäri-sivuston laitehallintaan lisätään laite "Home Assistant". Laitetta lisätessä sivustolla luodaan yksilöllinen laitetunnus (HAXXXXXXXXXX). Tämä laitetunnus tulee näkyviin Pörssäri-sivuston laitehallintaan kun laite on onnistuneesti lisätty.

Kyseinen laitetunnus lisätään Home Assistantissa input_text.porssari_mac -kentän arvoksi. Tämän jälkeen noin kahden minuutin kuluessa porssari_request-sensorin tulisi saada arvo 200 tai 304 merkkinä onnistuneesta palvelinkyselystä, ja puolen minuutin kuluessa tämän jälkeen muiden sensoreiden tulisi päivittyä. 

Onnistuneen palvelinkyselyn seurauksena Pörssäri-sivuston laitehallinnan Viimeksi nähty -aikaleima päivittyy vastaamaan nykyistä ajanhetkeä.

Yhteyskatkojen varalle on mahdollista ottaa käyttöön Telegram-viestisovellukseen integroitu yhteysvahti. Ohjeet tämän käyttöönottamiseksi löytyy osoitteesta https://porssari.fi/ohjeet/yhteysvahdin-kayttoonotto


### Ohjaus

Pörssäri-integraatio luo Home Assistantiin 8 kappaletta ohjaussensoreita, jotka saavat arvon 0 tai 1 sen perusteella kytketäänkö kyseinen tunti päälle vai pois. Näitä sensoreita voi käyttää automaatiotriggereinä Home Assistantin ohjaamien laitteiden päälle- ja poiskytkentään. 

Ohjausehtojen muokkaus suoritetaan toistaiseksi Pörssäri-sivuston laitehallinnan kautta valitsemalla Home Assistant -laitteen kohdalta "Muuta laitteen asetuksia". Kyseinen valinta avaa sivun, missä jokaisen kahdeksan ohjauskanavan senhetkiset asetukset ovat nähtävissä, ja niitä pääsee yksi kerrallaan muokkaamaan.

Päivitetyt asetukset haetaan Home Assistantiin seuraavan palvelinkyselyn yhteydessä. Home Assistantista suoritetaan palvelinkysely Pörssärin rajapintaan 1,5 - 2,5 minuutin välein.

Mikäli kanavalle ei ole määritetty ohjausparametreja Pörssäri-sivustolla, sensori saa arvon -1.
