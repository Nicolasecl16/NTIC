---
layout: default
title: default
description: default
---

[Retour sommaire](./)

# Principes théoriques de l'apprentissage semi-supervisé

L’objectif de cette partie est de mettre en lumière le fonctionnement théorique de l’apprentissage automatique et la place qu’il occupe dans le monde actuel du machine learning. L'apprentissage semi-supervisé est la branche de l'apprentissage machine qui consiste à utiliser des données étiquetées et non étiquetées pour effectuer certaines tâches d'apprentissage. Conceptuellement situé entre l'apprentissage supervisé et non supervisé, il permet d'exploiter des grandes quantités de données non étiquetées avec des ensembles de données étiquetées généralement plus petits. Ces dernières années, la recherche dans ce domaine a suivi les tendances générales observées dans l'apprentissage machine, avec une grande attention portée aux modèles basés sur les réseaux neuronaux. La littérature sur le sujet a également augmenté en volume et en portée, englobant maintenant un large spectre de théorie, d'algorithmes et d'applications.

## Contexte 

<p style='text-align: justify;'> 
On a pu voir dans la partie précédente à quel point l’annotation des données revêt une importance stratégique et économique dans le monde de l’IA. Les algorithmes semi-supervisés sont donc d’un grand intérêt dans l’optique d’annoter le mois de données possibles puisque seul une partie de l’ensemble d’entraînement est annoté. On peut également améliorer significativement un algorithme supervisé déjà existant, simplement en ajoutant des données non étiquetés à l’ensemble d’apprentissage. L'apprentissage semi-supervisé est récemment devenu plus populaire et plus pertinent sur le plan pratique en raison de la variété des problèmes pour lesquels de grandes quantités de données non étiquetées sont disponibles, par exemple du texte sur des sites web, des séquences de protéines ou des images
Ces caractéristiques expliquent certainement la résurgence dans la littérature des techniques d’apprentissage semi-supervisé. L’apprentissage semi-supervisé est ainsi mentionné  parmi les 10 tendances technologiques de 2020 identifiées par le monde informatique.
</p>
<p style='text-align: justify;'> 
Le tableau suivant propose un comparatif simple des méthodes d’apprentissage supervisés, semi-supervisés, et non supervisés. Cela permet de situer très grossièrement l’apprentissage semi-supervisé parmi les techniques d’apprentissage automatique actuelles.
</p>
<p align="center"><img src="img_rast.png" alt="img_rast" width="700"></p>

## Présentation introductive 
<p style='text-align: justify;'> 
Dans l'apprentissage machine, on distingue traditionnellement deux grandes tâches : l'apprentissage supervisé et l'apprentissage non supervisé. Dans l'apprentissage supervisé, on présente un ensemble de points de données composé d'une entrée x et d'une valeur de sortie correspondante y. L'objectif est alors de construire un classifieur ou un modèle de régression qui peut estimer la valeur de sortie pour des entrées autres que celles de la phase d’apprentissage. En revanche, dans l'apprentissage non supervisé, aucune valeur de sortie spécifique n'est fournie. Au lieu de cela, on essaie de déduire une structure sous-jacente à partir des entrées. Par exemple, dans le clustering non supervisé, l'objectif est de déduire une correspondance entre les entrées données (par exemple, des vecteurs de nombres réels) et des groupes de telle sorte que des entrées similaires soient mises en correspondance avec le même groupe. L'apprentissage semi-supervisé est une branche de l'apprentissage machine qui vise à combiner ces deux tâches. Généralement, les algorithmes d'apprentissage semi-supervisé tentent d'améliorer les performances dans l'une de ces deux tâches en utilisant des informations généralement associées à l'autre. Par exemple, lors de la résolution d'un problème de classification, des points de données supplémentaires pour lesquels l'étiquette est inconnue peuvent être utilisés pour faciliter le processus de classification. Pour les méthodes de clustering, en revanche, la procédure d'apprentissage peut bénéficier de la connaissance de l'appartenance de certains points de données à la même classe.
</p>
<p style='text-align: justify;'>  
Comme c'est le cas pour l'apprentissage machine en général, une grande majorité des recherches sur l'apprentissage semi-supervisé se concentre sur la classification. Les méthodes de classification semi-supervisée sont particulièrement pertinentes pour les scénarios où les données étiquetées sont rares. Dans ces cas, il peut être difficile de construire un classificateur supervisé fiable. Cette situation se produit dans des domaines d'application où les données étiquetées sont coûteuses ou difficiles à obtenir, comme le diagnostic assisté par ordinateur, la découverte de médicaments et le marquage de parties de discours. Si l'on dispose de suffisamment de données non étiquetées et sous certaines hypothèses concernant la distribution des données, les données non étiquetées peuvent aider à la construction d'un meilleur classifieur. 
</p>

## Fondements théoriques
<p style='text-align: justify;'> 
Dans les problèmes d'apprentissage supervisé traditionnels, on nous présente un ensemble ordonné de l points de données étiquetés <math> DL=((xi,yi))li=1…l </math>. Chaque point de données (xi,yi) est constitué d'un objet xi∈X provenant d'un espace d'entrée X donné, et a une étiquette associée yi, où yi est un réel dans les problèmes de régression et une classe dans les problèmes de classification. Sur la base d'un ensemble de ces points de données, généralement appelés données d’apprentissage, les méthodes d'apprentissage supervisé tentent de déduire une fonction qui peut déterminer avec succès l'étiquette y d'une entrée inédite x .
</p>
<p style='text-align: justify;'> 
Cependant, dans de nombreux problèmes de classification du monde réel, nous avons également accès à une collection de points de données u, <math> DU=((x<msub>i</msub>,y<msub>i</msub>))<msub>li=1…u</msub> </math>, dont les étiquettes sont inconnues. Par exemple, les points de données pour lesquels nous voulons faire des prédictions, généralement appelés données de test, ne sont pas étiquetés par définition. Les méthodes de classification semi-supervisées tentent d'utiliser des points de données non étiquetés pour construire un algorithme d’apprentissage dont la performance dépasse celle des algorithmes supervisés obtenus en utilisant uniquement les données étiquetées. Dans la suite de cette partie, nous appellerons XL et XU les entrées pour les échantillons respectivement étiquetés et non étiquetés.
</p>
<p style='text-align: justify;'> 
Il existe de nombreux cas où des données non étiquetées peuvent aider à construire un classifieur. Prenons, par exemple, le problème de la classification des documents, où l'on souhaite attribuer des sujets à une collection de documents textuels (des articles de presse). En supposant que nos documents soient représentés par l'ensemble des mots qui y figurent, on pourrait former un simple classifieur supervisé qui, par exemple, apprendrait à reconnaître que les documents contenant le mot "neutron" concernent généralement la physique. Ce classifieur pourrait bien fonctionner sur des documents contenant des termes qu'il a vus dans les données d'entraînement, mais il échouera lorsqu'un document ne contient pas de mots qui apparaissent dans l'ensemble d'entraînement. Par exemple, si nous rencontrons un document de physique sur les accélérateurs de particules qui ne contient pas le mot "neutron", le classifieur est incapable de le reconnaître comme un document concernant la physique. C'est là qu'intervient l'apprentissage semi-supervisé. Si nous considérons les données non étiquetées, il peut y avoir des documents qui relient le mot "neutron" à l'expression "accélérateur de particules". Par exemple, le mot "neutron" apparaît souvent dans un document qui contient également le mot "quark". En outre, le mot "quark" apparaît régulièrement avec l'expression "accélérateur de particules", ce qui guide les classifieurs dans la classification de ces documents comme étant également liés à la physique, bien qu'ils n'aient jamais vu l'expression "accélérateur de particules" dans les données étiquetées.
</p>
<p style='text-align: justify;'> 
La figure ci-dessous fournit une autre intuition quant à l'utilisation de données non étiquetées pour la classification. Nous considérons un problème de classification artificielle avec deux classes. Pour les deux classes, 100 échantillons sont tirés d'une distribution gaussienne bidimensionnelle avec des matrices de covariance identiques. L'ensemble de données étiquetées est ensuite construit en prélevant un échantillon de chaque classe. Tout algorithme d'apprentissage supervisé obtiendra très probablement comme limite de décision la ligne continue, qui est perpendiculaire au segment de ligne reliant les deux points de données étiquetés et qui la coupe au milieu. Cependant, ceci est assez loin de la limite de décision optimale. Comme le montre clairement cette figure, les clusters que nous pouvons déduire des données non étiquetées peuvent nous aider considérablement à placer la limite de décision : en supposant que les données proviennent de deux distributions gaussiennes, un simple algorithme d'apprentissage semi-supervisé peut déduire une limite de décision proche de l'optimum.
</p>
<p align="center"><img src="img_rast.png" alt="img_rast" width="700"></p>


## La main d’œuvre humaine omniprésente dans l’IA

<p style='text-align: justify;'> 
  La majorité du travail effectuée lors de la mise en place d’algorithmes d’intelligence artificielle est l’œuvre de l’homme. Plus précisément, les algorithmes supervisés dépendent de l’homme qui lui fournit des données étiquetés de qualité. Ces données sont ensuite utilisées lors de la phase d’apprentissage.
Selon une analyse de Cognilytica, plus de 80% du temps consacré aux projets en IA consiste à préparer et étiqueter les données.
</p>

<p align="center"><img src="img_rast.png" alt="img_rast" width="700"></p>

<p style='text-align: justify;'> 
  Selon un récent rapport de la société de recherche Cognilytica, plus de 35 entreprises fournissent actuellement de la main d’œuvre  pour ajouter des labels aux données afin d'alimenter les algorithmes d'apprentissage supervisé. Certaines de ces entreprises utilisent des approches générales d'étiquetage des données, tandis que d'autres font appel à leurs propres ressources humaines, gérées et formées, qui peuvent répondre à un large éventail de besoins généraux et spécifiques en matière d'étiquetage des données.  
</p>

## Le service en étiquetage de données, un secteur en pleine expansion
</p
<p style='text-align: justify;'>
L’émergence de l’IA et son omniprésence dans nos vies sont souvent sujettes à de nombreuses réserves. Une crainte majeure concernant la généralisation de l’IA est que non seulement les emplois disparaissent, mais que cette disparition affecte de manière disproportionnée les travailleurs peu qualifiés. Cela signifierait que tous les emplois nouvellement créés aillent à une élite d'employés de technologie tels que les développeurs de logiciels, les chercheurs en IA et les experts en cybersécurité.
Selon Guru Banavar, le chef de l'équipe d'IBM responsable de la création de Watson, l’une des IA les plus perfectionnées au monde, a déclaré récemment que ce ne sera pas nécessairement le cas.
</p>  
</p
<p style='text-align: justify;'> 
Banavar pense qu'il y aura "toutes sortes d'emplois disponibles" à l'ère de l'IA. Pour les travailleurs de tous les niveaux de compétences. Et pour les travailleurs moins qualifiés, l'informatique offre un nouveau champ de possibilités. 
Selon Banavar, c’est l’étiquetage de données qui sera le nouveau métier ouvrier du numérique,  et déclare ainsi « labellisation is the new blue-collar job ». Il appuie les conclusions présentées dans le graphique précédent et affirme ainsi « Si vous regardez les travaux d'analyse compliqués que nous avons aujourd'hui, 70% de ce travail consiste probablement à organiser et à nettoyer les données ».
</p>  
</p
<p style='text-align: justify;'>  
Selon le rapport de Cognilytica, la demande de services d'étiquetage de données par des tiers passera de 1,7 milliard de dollars (USD) en 2019 à plus de 4,1 milliards de dollars en 2024. Il s'agit d'un marché important, très éloigné de ce que l’on imagine en tant que futur de l’IA.
L'étiquetage des données pour l'apprentissage machine a donné naissance à une toute nouvelle industrie, et les sociétés qui se créent pour aider les entreprises à étiqueter leurs données font partie des investissements les plus populaires auprès des investisseurs en capital-risque qui espèrent tirer profit de la ruée vers l'or actuelle de l'I.A.
</p>

<p align="center"><img src="img_rast.png" alt="img_rast" width="700"></p>
</p
<p style='text-align: justify;'>
De nombreuses start-ups du milieu font aujourd’hui des levées de fond de grande envergure, augurant un futur très prometteur pour le secteur. Ceci explique la comparaison précédente issue du journal Fortune (Baker Hughes étant une entreprise parapétrolière américaine aujourd’hui valorisée à plusieurs dizaines de milliards de dollars)
Parmi ces entreprises, on peut citer  Labelbox, qui vient de lever 39 millions de dollars au cours de son second tour de financement.
Labelbox est en concurrence avec un certain nombre d'autres sociétés d'étiquetage : Scale AI, une autre plateforme d'étiquetage de données de San Francisco qui a recueilli 122 millions de dollars depuis sa création il y a trois ans, ainsi que des sociétés spécialisées dans la gestion d'équipes d'étiqueteurs de données, comme Hive, Cloudfactory et Samasource.
</p>

## d.	Annotation de données et modération de contenus

</p
<p style='text-align: justify;'>
Jusqu’ici, on a considéré l’annotation de données uniquement dans l’optique d’entraîner des algorithmes. Cependant, l’approche peut être différente : on emploie également des humains pour catégoriser des données car les machines n’en sont pas capables.
C’est dans ces situations qu’interviennent les modérateurs de contenu. Un reportage récent de France 2 dévoile à quel point le fait de donner un sens à un contenu est encore réservé à une main d’œuvre humaine. En effet, ce reportage, intitulé « Au secours, mon patron est un algorithme », nous dévoile que Facebook sous-traite à Accenture la modération des contenus publiés sur le site.  (Accenture est une entreprise de services française).  Les modérateurs doivent faire le tri des publications sur Facebook, et sont donc exposés aux textes et images les plus choquantes que l’on peut imaginer. Ce travail ne peut être effectué à l’heure actuelle par des algorithmes et soulève des problématiques éthiques à l’annotation des données. En effet, l’usure morale et psychologique des employés effectuant ce type de travail n’est pas encore reconnu.
</p>

<p align="center"><object width="560" height="315" src="//embedftv-a.akamaihd.net/e2f5e656431c5472722291a91db58096" ></object></p>

<h2 id="references">Références</h2>

<p>
  The Vital Edge, Data labeling for artificial intelligence in China, https://www.the-vital-edge.com/data-labeling-for-artificial-intelligence-in-china/
</p>
<p>
  Fortune, The human powered companies that make AI work, https://www.forbes.com/sites/cognitiveworld/2020/02/02/the-human-powered-companies-that-make-ai-work/#34cbd0f3670c
</p>
<p>
  France 2 , Cash investigation : « Au secours, mon patron est un algorithme » ,https://www.francetvinfo.fr/economie/emploi/metiers/video-cash-investigation-dans-la-peau-dun-moderateur-de-contenu-facebook_3623293.html
</p>
<p>
  Tech Republic, Is data labeling the new blue-collar job of the AI era?, https://www.techrepublic.com/article/is-data-labeling-the-new-blue-collar-job-of-the-ai-era/
</p>
<p>
  Fortune, If data is the new oil, these companies are the new Baker Hughes, https://fortune.com/2020/02/04/artificial-intelligence-data-labeling-labelbox/
</p>

