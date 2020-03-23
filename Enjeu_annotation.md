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
  <ul>
<li>Classification d’image</li>
<li>Reconnaissance vocale et reconnaissance de texte écrit</li>
<li>Analyse de sentiments</li>
<li>Pertinence et personnalisation de contenu</li>
</ul>

</p
<p style='text-align: justify;'> 
Les étiquettes peuvent se présenter sous la forme de délimitation autour des objets sur des images, d'un étiquetage visuel ou textuel des objets sur des photographies. Concernant  la reconnaissance vocale, il peut s’agir d’une transcription précise correspondant à un enregistrement audio.
L’ajout  d'étiquettes peut être un travail relativement peu qualifié (identifier les "chats" dans les vidéos) effectué par des milliers d'employés dans les centres d'externalisation traditionnels tels que l'Inde, la Roumanie ou les Philippines
Ces tâches d'étiquetage peuvent également nécessiter une main d’œuvre très qualifié dans d’autres cas. Par exemple, les entreprises de technologie médicale innovantes construisent des modèles d'apprentissage automatique qui peuvent identifier toutes sortes de problèmes sur les images médicales, tels que les caillots, les fractures, les tumeurs, les obstructions et autres problèmes. Pour construire ces modèles, il faut d'abord entraîner des algorithmes d'apprentissage automatique pour identifier ces problèmes dans les images. L’entraînement des modèles d'apprentissage machine nécessite de nombreuses données qui ont été étiquetées. Pour accomplir cette tâche d'étiquetage, il faut un certain niveau de connaissances sur la façon d'identifier un problème particulier et sur la façon de l'étiqueter de manière appropriée. Cette tâche n'est pas du ressort d'un individu pris au hasard. Cela nécessite une certaine expertise du domaine. En l’occurrence, il faudrait, dans ce cas précis, l’intervention de radiologues pour annoter correctement les données.
On peut également imaginer des annotations nécessitant l’intervention de spécialistes juridiques. Par exemple si l’on veut entraîner des algorithmes  détectant des clauses de non-confidentialité dans un contrat.
On constate donc que l’annotation des données recouvre des domaines très larges d’application

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
