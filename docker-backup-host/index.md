# Export de données (backup) de containers Docker 🐳


Il est possible d'exporter les données que l'on souhaite depuis Docker, c'est une utilisation intéressante notamment pour faire des backups !

Ici on ne parle pas de clusters ou de Ceph, juste d'un seul serveur qui fait tourner des containers (ou en local sur votre machine).

<br>

C'est une solution un peu naive mais qui a le mérite d'être facile à mettre en place lorsque l'on n'a qu'un seul serveur à gérer (par exemple pour un petit Homelab ou pour des projets qui n'ont pas besoin de scaler horizontalement ni d'avoir 99,99% d'uptime).

Il existe plusieurs manières de faire et celle que je vais décrire aujourd'hui consiste à exécuter une commande directement depuis le serveur qui fait tourner les containers Docker.

## Backup de volumes Docker 🐳

Le backup de volumes depuis la machine host est une tâche intéressante à effectuer car elle nécessite de comprendre comment les volumes docker peuvent être utilisés !

### Commande

```shell
docker run --rm -v nom_volume_docker:/mon_volume_point_montage:ro -v dossier_backup_host:/backup ubuntu tar cvf /backup/mon_backup_$(date "+%F-%Hh%M").tar /mon_volume_point_montage
```

### Explications

On commence par `docker run --rm -v nom_volume_docker:/mon_volume_point_montage:ro `
qui va consister à monter le volume du container que l'on souhaite sauvegarder ( en read only histoire de ne pas faire de bêtises 🤪) dans un autre container qui, lui, s'occupera d'effectuer un backup.

<br>

Ensuite, on a `-v dossier_backup_host:/backup ubuntu `,

ce qui signifie que notre container de backups ( ici Ubuntu ) montera aussi un dossier de l'host ( *dossier_backup_host* ), cette fois-ci en écriture, pour pouvoir envoyer le résultat du backup à cet endroit. 

<br>

Le résultat sera donc un dossier de backups dans l'host auquel s'ajoutera un nouveau fichier de backups généré à partir du volume docker à sauvegarder 😁.

C'est facultatif mais le tout peut être archivé ( ici au format tar), histoire de tout regrouper au même endroit dans une seule archive.

## Backup de base de données

Ici, je montre un exemple avec MySQL mais le principe est le même avec Postgres.

<br>

Pour éviter d'avoir à utiliser le mot de passe en clair dans la commande ou de le stocker en clair dans un script, on passe par l'utilisation des variables fournies dans le container de la base de données.

On peut par exemple passer par la variable `$MYSQL_PASSWORD` dans le cas de MYSQL. 

### Commande

Voici ce que ça donne :

```shell
docker ps | grep nom_container_db | awk '{print $1}' | xargs -I{} docker exec -i {} bash -c 'mysqldump -u$MYSQL_USER -p$MYSQL_PASSWORD $MYSQL_DATABASE --skip-comments --no-tablespaces' | gzip > mon_dump_genial_$(date "+%F-%Hh%M").psql.gz
```

### Explications

On commence par récupérer l'identifiant du container de notre base de données, de la manière suivante : ` docker ps | grep nom_container_db | awk '{print $1}'`. 

Il faudra bien penser à changer *nom_container_db* par le nom correct du  container. 
Puis, il suffit d'utiliser `xargs` combiné à `docker exec` pour envoyer notre commande de dump au container.

<br>

Cette commande utilise le programme `mysqldump` qui est fourni dans l'image docker officielle de `mysql`.
On a juste à placer les bons paramètres en précisant bien les variables d'environnement au bon endroit et on pourra récupérer le dump !

Enfin, on passe tout ça dans gzip histoire d'avoir un dump compressé.

<br>

*Note* : Dans le cas de l'utilisation d'un secret docker, il faudra passer par un chemin de type `/run/secrets/chemin_secret` et faire un `cat` sur ce chemin pour récupérer le mot de passe.

### Conclusion

Voilà comment faire des backups de containers simplement !
Il suffit ensuite de créer un petit script qui contient les deux commandes et de mettre le tout dans une tâche cron ( ou systemd ) pour faire des backups régulièrement 🙂.

Attention, pour une mise en production dans un cluster il faudra bien sûr utiliser une autre solution plus robuste ! 

