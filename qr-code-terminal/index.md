# Afficher et générer un QR Code depuis le terminal !


J'ai trouvé ce programme il y a très peu de temps et je le trouve vraiment sympa.
Je voulais donc partager ça avec vous !

<br>

### Utilisation

Le programme `qrencode` permet de générer des QR Code.
Ce qui est génial c'est qu'il permet de les générer dans plusieurs formats.

Pour générer une image, ça se fait de cette manière :

```shell
qrencode -o qrcode.png
```

### Affichage dans le terminal

Et là où j'ai vraiment trouvé la commande trop cool pour un geek comme moi, c'est qu'elle permet aussi de générer et d'afficher un QR Code directement dans le terminal 😁.

Pour afficher le QR Code directement depuis votre shell, ça se fait en précisant le type UTF8 ( qui permettra donc d'utiliser des caractères pour représenter le QR Code, au lieu d'une image ).


```shell
echo "https://brokenmatcha.com" | qrencode -t UTF8
```


### Vidéo

{{< rawhtml >}}
<blockquote class="tiktok-embed" cite="https://www.tiktok.com/@broken_matcha/video/7008926557586672902" data-video-id="7008926557586672902" style="max-width: 605px;min-width: 325px; margin: auto;" > <section> <a target="_blank" title="@broken_matcha" href="https://www.tiktok.com/@broken_matcha">@broken_matcha</a> <p>Générer un QR Code dans le terminal ! <a title="qrcode" target="_blank" href="https://www.tiktok.com/tag/qrcode">##qrcode</a> <a title="programmation" target="_blank" href="https://www.tiktok.com/tag/programmation">##programmation</a> <a title="dev" target="_blank" href="https://www.tiktok.com/tag/dev">##dev</a> <a title="edutok" target="_blank" href="https://www.tiktok.com/tag/edutok">##edutok</a> <a title="tiktokacademie" target="_blank" href="https://www.tiktok.com/tag/tiktokacademie">##tiktokacademie</a> <a title="linux" target="_blank" href="https://www.tiktok.com/tag/linux">##linux</a> <a title="informatique" target="_blank" href="https://www.tiktok.com/tag/informatique">##informatique</a> <a title="geek" target="_blank" href="https://www.tiktok.com/tag/geek">##geek</a> <a title="education" target="_blank" href="https://www.tiktok.com/tag/education">##education</a> <a title="developpeur" target="_blank" href="https://www.tiktok.com/tag/developpeur">##developpeur</a> <a title="techtok" target="_blank" href="https://www.tiktok.com/tag/techtok">##techtok</a></p> <a target="_blank" title="♬ lofi and minimalist BGM(325514) - Kazuhi" href="https://www.tiktok.com/music/lofi-and-minimalist-BGM-325514-6830448836784162818">♬ lofi and minimalist BGM(325514) - Kazuhi</a> </section> </blockquote> <script async src="https://www.tiktok.com/embed.js"></script>
{{< rawhtml >}}




