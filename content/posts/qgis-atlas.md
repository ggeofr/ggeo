---
author: ["P Guil"]
title: "Un atlas dans QGis"
date: "2025-05-13"
draft: "false"
description: "Un atlas dans QGis"
summary: "Utilisation des fonctions de base pour la réalisation de cartes en séries, pour l'export ou l'impression"
categories: ["sig"]
tags: [ "qgis" ]
ShowToc: true
TocOpen: true
social:
  bluesky_creator: "@ggeo.fr"
---
Utilisation des fonctions de base pour la réalisation de cartes en séries, pour l'export ou l'impression. Exemple d'un atlas communal des observations faunistiques. 

## Couche de couverture

Génération dynamique des cartes selon une couche d'emprise des cartes.

* selon des objets géographiques (communes, rivière, autour d'une éolienne)
* tuiles (créer une grille)

## Réalisation de la carte thématique

Insertion des:

* titre (dynamique)
* bloc de cartes
* échelle
* légende (filtrage)
* orientation
* logo

## Optimisation des échelles

dans les propriétés du projet

## 2 réglages de couches pour 2 cartes

* la carte thématique (atlas)
* la carte d'aperçu (aperçu)

## Paramétrage de l'atlas

* générer un atlas
* couche de couverture
* nom de page: champ du `"NOM"` de commune
* nom de fichier en sortie: `'Atlas_'||"NOM"`

## Modification du style d'aperçu pour la mise en évidence des objets

Ne pas utiliser la fonction d'aperçu mais modifier le style des entités (communes) avec des règles qui vont utiliser une variable: le nom de la page dynamique.

Les 2 règles sont définies par 2 filtres:  
`@atlas_pagename = "NOM"` représenté en rouge  
`@atlas_pagename <> "NOM"` représenté en blanc

## Filtrage de la légende

pour ne montrer que les entités à l'intérieur de l'entité de l'atlas

## Atlas sur 2 champs

Réalisation d'une série de cartes par espèce et par commune. Nécessité d'une couche d'entités avec 2 champs: espèces et communes  

* jointure spatiale entre source: couche de point des observations faunistiques et cible: les communes  
* paramétrage de l'atlas  
    couche de couverture: obs_faune_communes  
    nom de page:  `"taxon"||"NOM"`  
* filtre du style pour n'afficher qu'une espèce:  
    `@atlas_pagename = "taxon"||"NOM"`  

