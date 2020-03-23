---
layout: default
title: default
description: default
---

[Retour sommaire](./)

# Enjeu de l’annotation des données

## Intérêt de l’étiquetage

<p style='text-align: justify;'> 
L’étiquetage de données est typiquement utilisé dans les problèmes suivants :
- Classification d’image
-Reconnaissance vocale et reconnaissance de texte écrit
-	Analyse de sentiments
-	Pertinence et personnalisation de contenu

</p
<p style='text-align: justify;'> 
La rastérisation consiste à mapper uniquement les points de l'espace 3D visibles depuis la caméra sur le plan 2D qui constituera l'image finale. Le schéma ci-dessous a pour but de d'expliquer simplement les étapes clés.
</p>

<p align="center"><img src="img_rast.png" alt="img_rast" width="700"></p>

<p style='text-align: justify;'> 
  La première image montre la scène 3D telle qu'imaginée dans le jeu. Sur la deuxième image, on a gardé seulement les points des objets 3D visibles depuis la position de la caméra. Puis finalement chacun de ces points est projeté sur un plan 2D.
La deuxième étape est la plus cruciale, dans le sens où c'est elle qui minimise de façon conséquente le nombre de triangles à afficher sur l'image finale, grâce à des algorithmes de z-buffering, occlusion culling, etc. Aujourd'hui, en plus de produire des résultats très satisfaisants, ces calculs sont extrêmement efficaces, parallélisés sur GPU et optimisés par 3 décennies de développement.
</p>
<p style='text-align: justify;'> 
  Il y a cependant une limite au réalisme que peut atteindre la rastérisation. Comme on peut l'observer sur le schéma ce-dessus, seuls les objets visibles sont sélectionnés et mappés, tout autre objet du monde 3D n'a aucun impact sur l'image finale : un objet à la surface réfléchissante ne pourra projeter véritablement un objet en face de lui si celui-ci se trouve en dehors du champs de vision la caméra. Il existe évidemment des <i>hacks</i> qui permettent de simuler de tels effets, mais ceux-ci sont loin d'être réalistes. C'est là qu'intervient <a href="./raytracing.html"> le Ray-Tracing </a>. 
</p>

<h2 id="references">Références</h2>

<p>
  WIkipedia, Rasterisation, https://fr.wikipedia.org/wiki/Rast%C3%A9risation
</p>
<p>
  Microsoft, dirextX raytracing announce, https://devblogs.microsoft.com/directx/announcing-microsoft-directx-raytracing/
</p>
<p>
  NVidia, BRIAN CAULFIELD, https://blogs.nvidia.com/blog/2018/03/19/whats-difference-between-ray-tracing-rasterization/
</p>
