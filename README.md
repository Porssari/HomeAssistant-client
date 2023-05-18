# HomeAssistant-client
Pörssäri on mahdollista ottaa käyttöön myös Home Assistantin kautta. Home Assistant -laitteeseen lisätään automaattisesti 8 ohjauskanavaa, ja lisäksi käyttäjäkohtainen hintadata tuodaan käyttöön tuntirankeineen.

Esimerkki käyttöliittymästä (views.yaml):
![Example UI](/img/ui_example.png)

## Käyttöönotto
Lisää porssari_core.yaml sekä porssari_sensors.yaml -tiedostot Home Assistantin config-hakemistoon

Lisää seuraavat rivit configuration.yaml -tiedostoon:

```
homeassistant:  
  packages:    
    porssari_core: !include porssari_core.yaml    
    porssari_sensors: !include porssari_sensors.yaml

