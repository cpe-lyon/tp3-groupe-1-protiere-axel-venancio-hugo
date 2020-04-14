Axel Protiere
Hugo Venancio

# TP 3 - Gestion des paquets

## Exercice 1 : Commandes de base

Commencez par mettre à jour votre système avec les commandes vues dans le cours.
Donnez les commandes répondant aux questions suivantes :

1. Pour connaître les 5 derniers paquets installés sur votre machine il faut utiliser la commande ``` cat /var/log/dpkg.log | grep installed | tail -n 5``` . ```cat /var/log/dpkg.log``` affiche l'historique des installations sur les machines. ```grep installed ``` recherche le mot clé installed et ```tail -n 5``` affiche les 5 dernières lignes.

2. Pour connaître le nombre de paquet installés sur notre machine, on utilise la commande ```apt list --installed | wc -l ``` ou ``` dkpg --list | wc -l``` car apt et dkpg sont tout deux des gestionnaires de paquets. Ainsi, on envoie la liste des paquets au pipe qui en comptera le nombre  
grâce au ```wc -l```. Cependant, on constate une différence de 4. Cette différence s'explique car en tapant ```apt list --installed | head -n 5 ```, on remarque une ligne supplémentaire au début qui ne correspond pas à un paquet ``` en train de lister ... ``` donc le nombre ressortie par notre commande n'est pas exactement le nombre de paquet mais le nombre de paquet + 1. Et en tapant  ``` dkpg --list ``` on remarque qu'il y a 5 lignes supplémentaires au début qui sont ne sont pas des paquets donc le nombre ressorti par notre commande n'est pas exactement le nombre de paquet mais le nombre de paquet + 5. Ainsi, il y a donc une différence de 4. 

3.  Pour connaître le nombre de paquet disponible au téléchargement on exécute la commande  ``` apt list | wc -l  ```  auquel il ne faut pas oublier de soustraire 1 à cause de la ligne ``` en train de lister ... ```. La commande ```apt list``` envoie au pipe toute la liste des paquets disponibles et le pipe les compte avec ```wc -l```.

4. Pour mettre à jour le système, il faut faire ```apt upgrade ``` qui met à jour les paquets et ```apt update ``` qui met à jour les index. Ainsi, on a créé un alias qui réalise les deux commande en même temps avec ``` alias maj = apt upgrade; apt update```.

5. Le paquet ```fortune``` comporte des petites citations, des petits proverbes affichés à chaque connexion en mode console. Pour l'installer, il suffit d'utiliser ```sudo apt install fortune``` et à chaque commande ```fortune```, un proverbe s'affiche.

6. Pour rechercher le sudoku on utilise la commande ```apt search sudoku```. Ainsi, cette commande nous affiche tous les packages contenant sudoku . Il suffit alors dans choisir un et de l'installer avec ```apt install "nom du package"```.

7. Pour lister le nombre de package installé avec ```apt install``` on utilise la commande``` dpkg -S apt install``` qui nous ressort 476 packages installés.


## Exercice 2

Pour connaître le paquet qui a permis d'installer la commande ```ls```,  on tape la commande ```dpkg -S $(which -a ls)```. Cela nous renvoie un message d'erreur, puis le paquet qui a installé la commande avec l'emplacement de cette commande. Le paquet installé qui contient la commande ```ls``` est le paquet ```coreutils```. Ce dernier est un paquet contenant tous les outils de bases de Linux tels que ```cat```, ```ls```, ```rm```.

Le script ```origine-commande``` reprend la commande précédente pour obtenir les paquets ayant installé tout type de commande.
```
#!/bin/bash
dpkg -S $(which -a $1)
```

## Exercice 3
Ecrire une commande qui affiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du package
spécifié dans cette commande.

dpkg -l | grep "$1" 1>/dev/null && echo "INSTALLÉ" || echo "NON INSTALLÉ"
1>/dev/null redirige la sortie vers une corbeille

## Exercice 4

Pour lister les programmes livrés avec ```coreutils```, on affiche les informations sur le paquet et on affiche les 9 dernières lignes, qui contiennent les programmes livrés par le paquet. Pour cela, on exécute la commande ```apt show coreutils | tail -9```.

## Exercice 6

Nous avons donc installé la version Oracle de Java grâce aux commandes stipulées par l'énoncé. Le fichier ```linuxuprising-ubuntu-java-bionic.list``` a été créé  dans le répertoire ```etc/apt/sources.list.d```

La commande ```[``` est une commande de test booléen. Utilisée ainsi ```[ EXPRESSION ]```, elle vérifie la validité de l'expression en retournant le statut de sortie. La valeur 0 correspond à un vrai et 1 à un faux.
