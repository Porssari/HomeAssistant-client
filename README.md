# HomeAssistant-client
Pörssäri Home Assistant integration

![Example UI](/img/ui_example.png)

## Käyttöönotto
Lisää porssari_core.yaml sekä porssari_sensors.yaml -tiedostot Home Assistantin config-hakemistoon

Lisää seuraavat rivit configuration.yaml -tiedostoon:

```
homeassistant:  
  packages:    
    porssari_core: !include porssari_core.yaml    
    porssari_sensors: !include porssari_sensors.yaml

