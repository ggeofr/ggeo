---
author: ["P Guil"]
title: "Vidéo au démarrage avec un Raspberry Pi"
date: "2025-05-11"
draft: "false"
description: "Vidéo au démarrage avec un Raspberry Pi"
summary: "Utilisation et paramétrage d'un Raspberry Pi pour la lecture d'une vidéo en continue pour servir de borne vidéo autonome dans un musée"
categories: ["informatique"]
tags: [ "linux", "raspberrypi" ]
ShowToc: true
TocOpen: true
social:
  bluesky_creator: "@ggeo.fr"
---
# Comment lancer un script ou une vidéo au démarrage d'un ordinateur Raspberry?

## Installer le raspberry

Télécharger Raspberry Pi Imager pour télécharger et flasher la carte SD du raspberry
<https://www.raspberrypi.org/downloads/>

Avec ce logiciel disponible sous Windows, Linux et Mac, choisir l'image à télécharger: prendre Raspberry Pi OS Lite (sans GUI), et choisir la carte SD à flasher.

## Premier démarrage du raspberry

utilisateur: pi
mot de passe: raspberry
adresse IP à lire pendant le démarrage en ayant au préalable un écran HDMI branché.

## Activer SSH

Activer SSH depuis le Raspberry Pi avec raspi-config.
Première solution pour activer SSH, votre Raspberry Pi possède un écran et un clavier. Dans ce cas, nous allons directement utiliser l’outil en ligne de commande raspi-config.

Ouvrez un terminal, et tapez-y la commande suivante :

```bash
sudo raspi-config
```

Raspi-config est un outil permettant de gérer de nombreuses options sur Raspbian.
Si vous ne l’avez pas fait, je vous conseille de commencer par changer le mot de passe par défaut (première ligne, « Change user password ») du Raspberry Pi puisqu’il sera désormais accessible en SSH.

Puis, une fois le mot de passe changé, allez dans la partie « Interfacing Options » et choisissez la ligne SSH, puis « Yes ».

Et voilà, votre serveur SSH est activé !

## Télécharger la vidéo

Pour commencer, nous allons télécharger une vidéo à l’aide de youtube-dl que j’ai présenté ici si vous ne l’avez pas installé.
Ouvrez un terminal et tapez ce qui suit :

```bash
youtube-dl -f mp4 https://www.youtube.com/watch?v=XoDY9vFAaG8
```

La vidéo choisie est top, vous verrez 😉
Garder à l’esprit l’endroit ou la vidéo s’est enregistrée (normalement dans le répertoire pi).

Nous renommons notre vidéo pour que ça soit plus simple :

```bash
rm https://www.youtube.com/watch?v=XoDY9vFAaG8 martinpecheur.mp4
```

## Copier la vidéo avec ssh et SCP

## Installer omxplayer

```bash
sudo apt install omxplayer
```

Ensuite nous allons créer un dossier pour placer notre vidéo et plus tard notre bout de code.

```bash
mkir video
mv loop.mp4 video/
cd video/
```

## Créer le script:

```bash
sudo nano start.sh
```

Et copiez ceci à l’intérieur du fichier qui s’ouvre :

```bash
#!/bin/sh
omxplayer --loop -o hdmi -b /home/pi/video/martinpecheur.mp4
```

Quitter en appuyant sur ctrl+x et faite « o » ou « y » pour confirmer l’enregistrement.
Le script indique que la vidéo située dans le répertoire loop/ s’ouvrira avec omxplayer en boucle avec le son sur l’hdmi.

On met le script exécutable :

```bash
sudo chmod +x start.sh
```

On fait un test pour voir si ça se lance :

```bash
./start.sh
```

## Pour que la vidéo se lance au démarrage du pi utiliser crontab

```bash
sudo crontab -e
```

Spécifier l'éditeur de texte comme nano. Ecrire les lignes suivantes :

```bash
@reboot sh /home/pi/video/start.sh
```

Sauvegardez et quittez avec ctrl+x et « o » ou « y ».

## Lancer le raspberry

Pour redémarrer:

```bash
sudo reboot
```

ou pour éteindre proprement le raspberry pi:

```bash
sudo shutdown -h now
```

## Arrêter le script pendant qu’il tourne avec ssh

Une fois connecté en ssh (depuis votre smartphone par ex), la commande « top » va nous indiquer quels sont les processus en cours :

`top`

Repérez le numéro ID d’omxplayer (par exemple 611) et nous y mettons fin avec la commande suivante :

`kill 611`
