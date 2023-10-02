

### Les modèles structurels vous guident pour assembler des objets et des classes en de plus grandes structures tout en gardant celles-ci flexibles et efficaces

#### Il y à 4 modèles structurels :

- Adaptateur
- Décorateur
- Composite
- Façade



### Pattern Adaptateur

**Objectif :**

Convertir l’interface d’une classe en une autre conforme à l’attente du client.

**Utilisation :** 

- On veut utiliser une classe existante, mais dont l’interface ne coïncide pas avec celle escomptée.

- On souhaite créer une classe réutilisable qui collabore avec des classes sans relations avec elle et encore inconnues.


**Solution :**

- l’adaptateur implémente l’interface d’un objet et en encapsule un autre.

![[Pasted image 20231002090115.png]]



**Exemple :**

- Voici une première version d’un jeu vidéo, le jeu a été conçu pour être jouable avec une « manette» (joystick).


![[Pasted image 20231002090157.png]]

Nous désirons mettre à jour le jeu pour permettre également le jeu au clavier, avec le minimum d’impact sur le code existant.

Voici la classe Clavier fournie:

```java
public class Clavier { public enum Key { SPACEBAR, ARROW_LEFT, ARROW_RIGHT, ... };
					  
public Clavier() 
{
/* constructeur */ 
} 
public Key keyPressed()
{
/* retourne le type de la touche */ 
}
/* etc */ 
}
```


### Pattern Décorateur (Wrapper)

**Objectif :** 

- Attacher dynamiquement des responsabilités supplémentaires à un objet. Alternative à la dérivation pour étendre des fonctionnalités.


**Utilisation :** 

- Pour ajouter des responsabilités sans affecter les autres objets.
- Pour retirer des responsabilités.
- Quand l’extension par dérivation est impraticable du fait du trop grand nombre de sous-classes qu’il faudrait créer.


**Solution :** 

- Décorateur définit une interface conforme à celle du Composant et gère une référence à un objet Composant. Il peut ainsi transmettre les requêtes à son objet Composant mais aussi effectuer des opérations supplémentaires avant ou après la transmission de la requête.


![[Pasted image 20231002090510.png]]


**Exemple :**

- On a développé un programme permettant de lire et d’écrire des données dans un fichier.

![[Pasted image 20231002090538.png]]


Sans modifier le code existant, on souhaite modifier la manière dont les données sont lues et écrites.

- Dans certains cas, on voudra que les données soient cryptées avant d’être écrites et décryptées après être lues. 

- Dans d’autres cas, on voudra que les données soient compressées avant d’être écrites et décompressées après être lues.

- Parfois on souhaitera faire les deux.


### Pattern Composite

**Objectif :**

- Agencer les objets dans des arborescences afin de pouvoir traiter celles-ci comme des objets individuels.

**Utilisation :**

- doit être réservé aux applications dont la structure principale peut être représentée sous la forme d’une **arborescence**.
- On souhaite que le client n’ait pas à se préoccuper de la différence entre une combinaison d’objets et des objets individuels.

**Exemple :**

- Des menus sont composés d’éléments de menus, chacun pouvant être un élément simple ou un menu.
- Des répertoires contiennent des éléments pouvant être des fichiers mais aussi des répertoires. 
- Des figures sont composées d’éléments primitifs, des points, des lignes, des cercles, mais aussi d’autres figures.

**Solution :**

- Composer des objets en des structures arborescentes pour représenter des hiérarchies composant/composé
![[Pasted image 20231002100459.png]]


### Pattern Façade

**Objectif :**

- Simplifier l’utilisation d’un sousensemble d’un système complexe existant ou proposer un moyen de ne manipuler le système que d’une manière spécifique.

**Utilisation :** 

- On souhaite disposer d’une interface simple pour utiliser un sous-ensemble d’un système complexe

- On veut structurer un système en plusieurs couches. Créez des façades pour définir des points d’entrée à chaque niveau du système.

- Une façade se révèle très pratique si votre application n’a besoin que d’une partie des fonctionnalités d’une librairie sophistiquée parmi les nombreuses qu’elle propose.

- On souhaite masquer le système d’origine.


**Solution :**

- Faire communiquer les clients avec le système en envoyant des requêtes à la façade qui répercute celles-ci aux objets appropriés du système. La façade offre une interface spécialisée plus facile à utiliser.

#### Implémentation :

1. Définir l'interface requise
2. Créer une classe implémentant l’interface à l’aide des fonctionnalités du système existant.

![[Pasted image 20231002090832.png]]


