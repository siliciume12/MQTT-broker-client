# MQTT-broker-client

# Materiel
- ESP-32 (sublisher)
- ESP-32 (publisher)
- Rasberry (broker)
- Machine linux (IHM-publishert-sublisher)

# Descriptrif du projet

Dans ce github vous verez comment installer un reseau MQTT-mosquitto. Les appareils communicant seront un esp32 qui va pouvoir envoyer la température d'un bmp280 vers un broker.
Un autre ESP-32 subcriber va recevoir les donnés de température ainsi qu'une machine linux (toujours sur le reseaux local) qui va voir et publier des messages. 
