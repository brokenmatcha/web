# Séléction de colonnes avec AWK


## Présentation

**AWK** est un programme très impressionnant qui permet de faire beaucoup de choses et qui complète bien l'ensemble d'outils disponibles dans un shell Unix.

C'est un outil important à connaitre lorsqu'on manipule les lignes de commandes, c'est un peu le SQL de la ligne de commandes 😀.

## Utilisation
Je l'utilise principalement pour sélectionner une colonne et/ou une ligne depuis le terminal.

En effet, **awk** est très utile en tant que programme permettant de faire des requêtes de texte.
C'est un peu comme si c'était des requêtes SQL dans une base de données mais au lieu d'avoir une base de données on travaille sur du texte.

Et vu que sur les systèmes Unix, on manipule *énormément* de texte, ça en fait un outil excellent et très puissant !

## Exemple

### Récupérer l'identifiant docker d'un container en particulier

Par exemple, la commande `docker ps` donne une liste de containers qui tournent actuellement sur un host donné.

```shell
CONTAINER ID   IMAGE                                                 COMMAND                  CREATED       STATUS              PORTS                                                                                                                                 NAMES
629d19dd2f68   docker.elastic.co/elasticsearch/elasticsearch:7.9.3   "/tini -- /usr/local…"   3 days ago    Up 8 hours          9200/tcp, 9300/tcp                                                                                                                    dev_es_1
1ec5572d20fe   thecodingmachine/gotenberg:6                          "/tini -- gotenberg"     3 days ago    Up 8 hours          3000/tcp                                                                                                                              dev_gotenberg-1
657e688f32df   mysql:5.7   
```

<br>

Si je souhaite sélectionner l'identifiant du container Elasticsearch, je peux utiliser **awk** pour récupérer seulement la colonne correspondant à l'identifiant !

Ce qui se ferait de la manière suivante :

### 1. Récupérer la bonne ligne
Il y a plein de manières de récupérer une ligne mais grep semble en général la solution la plus simple.
Tout d'abord donc, je récupère la ligne correspondante à elasticsearch avec un filtre `grep elasticsearch`.

<br>

Ce qui nous donne plus que la ligne :
```shell
629d19dd2f68   docker.elastic.co/elasticsearch/elasticsearch:7.9.3   "/tini -- /usr/local…"   3 days ago    Up 8 hours          9200/tcp, 9300/tcp                                                                                                                    dev_es_1
```


### 2. Récupérer la bonne colonne
Une fois la ligne récupérée, je peux ensuite utiliser **awk** pour ne garder que la colonne correspondant à l'ID du container !

<br>

Ce qui donne la commande :

```shell
docker ps | grep elasticsearch | awk '{print $1}'
```

On obient `629d19dd2f68` qui correspond bien à notre identifiant recherché !

<br>

On peut ensuite combiner le tout avec `xargs` pour par exemple stopper le container 😁.

## Aller plus loin

Ce qui est génial c'est que **awk** fournit plein d'outils pour faire les meilleures requêtes possibles.

<br>

Par exemple:
- pour récupérer la troisième ligne on peut utiliser `awk 'NR==3' {print}'`
- pour récupérer les lignes 3 à 5 on peut utiliser `awk 'NR>=3 && NR<=5 {print}'`
- pour récupérer la dernière colonne on utilisera `awk '{print $NF}'`.
- etc ...

Un article plus détaillé sur **awk** pourrait peut-être être intéressant 🤔.

<br>

# Vidéo

{{< rawhtml >}}
<blockquote class="tiktok-embed" cite="https://www.tiktok.com/@broken_matcha/video/7005208966020058373" data-video-id="7005208966020058373" style="max-width: 605px;min-width: 325px; margin:auto;" > <section> <a target="_blank" title="@broken_matcha" href="https://www.tiktok.com/@broken_matcha">@broken_matcha</a> <p>Sélectionner une colonne avec awk !  #<a title="education" target="_blank" href="https://www.tiktok.com/tag/education">#education </a>#<a title="linux" target="_blank" href="https://www.tiktok.com/tag/linux">#linux </a>#<a title="learnontiktok" target="_blank" href="https://www.tiktok.com/tag/learnontiktok">#learnontiktok </a>#<a title="tiktokacademie" target="_blank" href="https://www.tiktok.com/tag/tiktokacademie">#tiktokacademie </a>#<a title="informatique" target="_blank" href="https://www.tiktok.com/tag/informatique">#informatique </a>#<a title="programmation" target="_blank" href="https://www.tiktok.com/tag/programmation">#programmation </a>#<a title="developpeur" target="_blank" href="https://www.tiktok.com/tag/developpeur">#developpeur </a>#<a title="shell" target="_blank" href="https://www.tiktok.com/tag/shell">#shell </a>#<a title="geek" target="_blank" href="https://www.tiktok.com/tag/geek">#geek </a>#<a title="code" target="_blank" href="https://www.tiktok.com/tag/code">#code</a></p> <a target="_blank" title="♬ Coffee - LoFi Hip Hop" href="https://www.tiktok.com/music/Coffee-6789323932156561409">♬ Coffee - LoFi Hip Hop</a> </section> </blockquote> <script async src="https://www.tiktok.com/embed.js"></script>
{{< rawhtml >}}


