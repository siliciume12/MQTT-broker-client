![texte alternatif](images/photo.png)




# MQTT-broker-client

# Materiel
- ESP-32 (sublisher)
- ESP-32 (publisher)
- Rasberry (broker)
- Machine linux (IHM-publishert-sublisher)

# Descriptrif du projet

Dans ce github vous verez comment installer un reseau MQTT-mosquitto. Les appareils communicant seront un esp32 qui va pouvoir envoyer la température d'un bmp280 vers un broker.
Un autre ESP-32 subcriber va recevoir les donnés de température ainsi qu'une machine linux (toujours sur le reseaux local) qui va voir et publier des messages. 

# instruction installations broker
Étape I : installation du Broker 

	Pour commencer on installe les dépendances MQTT  sur l’appareil qui servira de serveur.
Le matériel utiliser sera essentiellement du Linux, donc les commande seront en bash.

Ouverture du terminal de commande Rasberry-pi

Les étapes sont les suivantes :

## 1. Mettre à jour le système

sudo apt update && sudo apt upgrade -y
```

## 2. Installer Mosquitto complet (broker + clients)

sudo apt install mosquitto mosquitto-clients -y
```

* mosquitto : le broker MQTT
* mosquitto-clients`: outils `mosquitto_pub` et `mosquitto_sub`

## 3. Démarrer et activer le service 

Demarre mosquitto
sudo systemctl start mosquitto 

Le lance dés le démmarrage du rasberry-pi
sudo systemctl enable mosquitto

Verifie sont statut
sudo systemctl status mosquitto



## 4. Configurer pour accès local et distant



sudo nano /etc/mosquitto/mosquitto.conf


Ajouter ou modifier :

listener 1883
allow_anonymous true
include_dir /etc/mosquitto/conf.d
```

Puis redémarrer :

```bash
sudo systemctl restart mosquitto


## 5. Tester en local

* Subscriber :


mosquitto_sub -h localhost -t "test/topic"
```

* Publisher :

mosquitto_pub -h localhost -t "test/topic" -m "Bonjour Pi!"


## 6. Tester depuis un autre PC sur le même réseau

1. Trouver l’IP du Pi (broker):


hostname -I
```

2. Sur le PC externe (autre pc linux):

Met en écoute de le pc externe
mosquitto_sub -h <IP_du_Pi> -t "test/topic"

Sur un autre cmd
mosquitto_pub -h <IP_du_Pi> -t "test/topic" -m "Hello depuis le PC"

## 7. Notes importantes

* `allow_anonymous true` : pratique pour tester mais pas sécurisé
* Pour sécuriser le broker : utiliser `mosquitto_passwd` et configurer `allow_anonymous false`
* Sur Raspberry Pi, possibilité de connecter des capteurs (DHT22, BMP280) et publier leurs données via MQTT


##.8 installer mqttX sur rasberry pi ou linux amd

Suivre le liens ci-dessous et télécharger la version correspondante à votre appareil (exemple d’IHM de mqtt).
https://mqttx.app/downloads
