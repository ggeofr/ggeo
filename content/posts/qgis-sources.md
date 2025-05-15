---
author: ["P Guil"]
title: "Réparer les sources de données dans QGis"
date: "2025-05-14"
draft: "false"
description: "Réparer les sources de données dans QGis"
summary: "Réparer les sources de données dans QGis"
categories: ["sig"]
tags: [ "qgis" ]
ShowToc: true
TocOpen: true
social:
  bluesky_creator: "@ggeo.fr"
---
## QGis Windows -> QGis Linux

Pour réparer la source de données dans QGis

Extention `changeDataSource`

remplacer:
`S:\`

par:
`/run/user/1000/gvfs/smb-share:server=pmpad,share=sig/`

puis remplacer `\` par `/`
