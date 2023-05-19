# HomeAssistant-client
Pörssäri on mahdollista ottaa käyttöön myös Home Assistantin kautta. Home Assistant -laitteeseen lisätään automaattisesti 8 ohjauskanavaa, ja lisäksi käyttäjäkohtainen hintadata tuodaan käyttöön tuntirankeineen.

Esimerkki käyttöliittymästä (views.yaml):

![Example UI](/img/ui_example.png)

### Käyttöönotto
Lisää porssari_core.yaml sekä porssari_sensors.yaml -tiedostot Home Assistantin config-hakemistoon

Lisää seuraavat rivit configuration.yaml -tiedostoon:

```yaml
homeassistant:  
  packages:    
    porssari_core: !include porssari_core.yaml    
    porssari_sensors: !include porssari_sensors.yaml
```

Sivustolle laitetta lisätessä luodaan yksilöllinen laitetunnus HAXXXXXXXXXX. Kyseinen laitetunnus lisätään text input -Pörssäri laitetunnuksen arvoksi minkä jälkeen request-sensorin tulisi saada arvo 200 tai 304 merkkinä onnistuneesta palvelinkyselystä. Lisäksi sivuston viimeksi nähty -aikaleima tulisi päivittyä vastaamaan nykyistä ajanhetkeä.


### Ohjaus

Pörssäri-integraatio luo Home Assistantiin 8 kappaletta ohjaussensoreita, jotka saavat arvon 0 tai 1 sen perusteella kytketäänkö kyseinen tunti päälle vai pois. Näitä sensoreita voi käyttää automaatiotriggereinä Home Assistantin ohjaamien laitteiden päälle- ja poiskytkentään. Mikäli kanavalle ei ole määritetty ohjausparametreja Pörssäri-sivustolla, sensori saa arvon -1.


### Hintatiedot
Ohjaustiedon mukana toimitetaan myös käyttäjäkohtainen hintatieto. Esimerkki hintatiedon käytöstä löytyy porssari_sensors.yaml -tiedoston sensoreista. 

Esimerkki json-ohjausdatan rakenteesta hintatiedon osalta:

```json
"Prices": {
  "2023-05-18T00:00:00+0300": {
    "Price":"8.11",
    "Rank_cheap":"5",
    "Rank_Expensive":"18"
  },
  "2023-05-18T01:00:00+0300": {
    "Price":"8.10",
    "Rank_cheap":"4",
    "Rank_Expensive":"19"
  },
  "2023-05-18T02:00:00+0300": {
    "Price":"8.03",
    "Rank_cheap":"2",
    "Rank_Expensive":"21"
  }
}
```
