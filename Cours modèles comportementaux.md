### Les modèles comportementaux s’occupent des algorithmes et de la répartition des responsabilités entre les objets.



### Patterns :

1. Stratégie
2. Patron de méthode
3. Observateur
4. Commande
5. Etat
6. Itérateur
7. Chaîne de responsabilité
8. Visiteur


### Le pattern Stratégie

**Objectif :** 

- Définir une famille d’algorithmes, encapsuler chacun d’eux et les rendre interchangeables en fonction du contexte.

**Solution :**

- séparer la sélection de l’algorithme de son implémentation. La sélection est basée sur le contexte

- Le contexte peut fournir à la stratégie toutes les données que requiert l’algorithme.

- Le contexte peut se communiquer lui-même en tant qu’argument aux opérations de Stratégie.

![[Pasted image 20231002091136.png]]


**Utilisation :**

- On a besoin de diverses variantes d'un algorithme

- Un algorithme utilise des données que les clients n'ont pas à connaître

- Une classe définit de nombreux comportements, qui figurent dans ses opérations sous forme de déclaration conditionnelles multiples.

##### Un des exemples du pattern Stratégie dans l’API JAVA permet la définition de plusieurs stratégies de comparaison avec l’interface Comparator :

```java
public Comparator{ public int compare(T o1, T o2); }
```

- Utilisation pour définir un autre ordre que l'ordre naturel dans un ```java SortedSet<E>

```java
public TreeSet( Comparator c)
```

- Utilisation dans la classe Collections

```java
public static void sort( List list, Comparator c)
```



```java
public class Test {
public static void main (String[] args){
List<String> liste = new ArrayList<>();
liste.add('abc');
liste.add('c');
liste.add('ab');
//tri de la liste suivant l'ordre lexicologique
Collections.sort(liste);
//tri de la liste suivant la longueur des mots
Collections.sort(liste, new Comparator<String>(){
	public int compare (String s1, String s2){return s1.length() - s2.length();}})
	}
}
```

### Patron de méthode

**Objectif :**

- Définir, dans une opération, le squelette d’un algorithme, en en déléguant certaines étapes à des sous-classes. Redéfinir par des sous-classes certaines parties d’un algorithme sans avoir à modifier la structure de ce dernier.

**Solution :**

- Permettre la définition de sousétapes variant tout en conservant un processus de base cohérent.

**Utilisation :**

- Implémenter une fois pour toute les parties invariantes d’un algorithme.

- Pour éviter la duplication de code, on va chercher le facteur commun des comportements des sousclasses et l’implanter dans une classe commune.

![[Pasted image 20231002092519.png]]

**Comparaison Patron méthode / Stratégie :**

- Le patron de méthode utilise l’héritage pour modifier une partie d’un algorithme.

- Les stratégies utilisent la délégation pour modifier l’algorithme tout entier.

**Exemple : Jeux à deux joueurs humains**

On souhaite créer une application permettant de jouer une partie de jeu de Nim ou une partie de jeu Puissance 4. Au début du jeu, on choisit le jeu puis on saisit les noms des deux joueurs. Pour le jeu de Nim, il faut préciser le nombre de tas de la partie.

**Exemple : Jeux à deux joueurs humains ou contre l’IA**

On souhaite maintenant proposer de jouer contre l’IA ou à deux joueurs humains. Pour le jeu de Nim, on envisage deux modes de jeux pour l’IA, soit il applique la stratégie gagnante soit une stratégie aléatoire parmi tous les coups possibles.


### Pattern Observateur

**Objectif :**

- Définit une dépendance de type un à plusieurs, de façon telle que, quand un objet change d’état, tous ceux qui en dépendent en soient notifiés et automatiquement mis à jour

**Exemple 1 :**

- On veut proposer plusieurs représentations d’un même ensemble de données. Par exemple, en utilisant un objet tableur, en utilisant un objet histogramme. On peut vouloir ajouter d’autres types de représentations. Quand les données changent, les représentations doivent se mettre à jour.

![[Pasted image 20231002093141.png]]



**Solution :**

- Les **observateurs** délèguent la responsabilité de contrôle d’un événement à un objet central, le sujet. Chaque fois que **le sujet** change d’état, il envoie une notification à tous ses observateurs. 
- Chaque observateur interrogera le sujet sur son état.

![[Pasted image 20231002093233.png]]


![[Pasted image 20231002093246.png]]

**Utilisation :**

- Quand la modification d’un objet nécessite d’en modifier d’autres mais qu’on ne sait pas combien sont ces autres.
- Quand un objet doit faire des notifications à d’autres objets sans faire d’hypothèse sur la nature de ces objets.

**Modèle Push :** le sujet peut transmettre les données nécessaires aux observateurs en paramètre de la méthode ``mettreAJour()``.

**Modèle Pull :** le sujet n’envoie aucune donnée à ses observateurs qui demanderont ensuite les données dont ils ont besoin.

- Dans certains cas, on peut identifier des événements qui intéressent uniquement certains observateurs. Chaque observateur s’inscrit auprès du sujet en indiquant les événements qui l’intéressent. Quand un événement survient, le sujet n’informe que les observateurs inscrits pour ce type d’événement.

- Dans certains cas, il peut être nécessaire de confier à un objet intermédiaire certaines vérifications avant notification aux observateurs surtout quand un observateur observe plusieurs sujets. Cela évite les notifications redondantes. L’objet GereModifs va maintenir une table SujetObservateurs.

![[Pasted image 20231002093428.png]]


**Conséquences :**

- On peut réutiliser les sujets sans réutiliser les observateurs et réciproquement.
- On peut ajouter un observateur sans avoir à modifier le sujet ni les autres observateurs.

**Exemple 2 :**

- On veut créer une application permettant d’afficher de trois façons différentes des données météorologies. On pourra vouloir ajouter d’autres affichages ultérieurement. On considère un objet DonneesMeteo qui enregistre les données météorologiques à un moment donné (température, hydrométrie et pression atmosphérique). On souhaite afficher les données complètes actuelles, les statistiques et des prévisions simples.

![[Pasted image 20231002093534.png]]


### Pattern Commande


**Objectif :**

- Prendre une action à effectuer et la transformer en un objet autonome qui contient tous les détails de cette action. Cette transformation permet de paramétrer des méthodes avec différentes actions, planifier leur exécution, les mettre dans une file d’attente ou d’annuler des opérations effectuées.

**Solution :**

- Découpler l’objet qui invoque l’opération de celui qui a la connaissance nécessaire pour réaliser cette opération. L’objet qui émet la requête n’a à connaître que la façon de l’émettre; il n’a pas besoin de savoir comment la satisfaire.

**Exemple 1 :**

- On souhaite concevoir une boîte à outils permettant de créer facilement une interface utilisateur pour tous types d’applications.
- Cette boite à outils comportera des boutons, des menus, des raccourcis claviers.
- Tous ces éléments exécutent une requête en réponse à une entrée utilisateur.

**Exemple 1 - Points à prendre en compte pour la conception :**

- On ne connaît pas le destinataire d’une requête ni les opérations qu’il doit exécuter.
- Plusieurs éléments de l’interface (bouton, élément de menu) exécutent la même requête.

**Exemple 1 - Solution :**

- Transformer la requête en un objet.
- Définir une interface Commande pour l’exécution des opérations avec une seule méthode ``execute()``.
- Définir les requêtes concrètes en créant des classes qui implémentent l’interface Commande et qui stockent le récepteur et l’action qu’il doit exécuter.
- Relier les commandes particulières aux boutons ou autres éléments suivant le comportement attendu quand on clique dessus.

![[Pasted image 20231002093742.png]]

![[Pasted image 20231002093754.png]]

**Utilisation :**

- Introduire dans des objets, sous la forme de paramètres, des actions à effectuer.
- Spécifier, mettre en file d’attente et exécuter des requêtes à différents instants.
- Proposer le service « défaire » (undo). Dans ce cas, l’interface Commande contient une méthode ``undo()`` qui supprime les effets d’un précédent appel à ``execute()``. Les commandes exécutées sont stockés par l’invocateur dans une liste historique.


**Exemple 2 :**

- On considère la classe Calculatrice permettant de réaliser les opérations suivantes : addition, soustraction, multiplication et division.
- On souhaite proposer un menu permettant d’effectuer une suite d’opérations puis d’afficher le résultat. On veut également pouvoir annuler un certain nombre d’opérations.

```java
public class Calculatrice{
	private int valeurCourante;

	public int getValeurCourante(){
		return valeurCourante;
	}

	public void operation(char operation,int operande){
		switch(operation)
		{
			case '+': valeurCourante += operande;break;
			case '-': valeurCourante -= operande;break;
			case '*': valeurCourante *= operande;break;
			case '/': valeurCourante /= operande;break;
		}
	
	}
@Override
	public String toString(){
	return String.valueOf(valeurCourante);
	}
}
```

### Pattern Etat


**Objectif :**

- Permet à un objet de modifier son comportement quand son état interne change.

**Solution :**

- Traiter l’état de l’objet comme un objet à part entière en définissant des classes concrètes correspondant à tous les états possibles et partageant une interface commune.
- L’objet original que l’on nomme *contexte*, stocke une référence vers un des objets état qui représente son état actuel. Il délègue tout ce qui concerne la manipulation des états à cet objet.

![[Pasted image 20231002094408.png]]

**Utilisation :**

- Le comportement d’un objet dépend de son état et ce changement de comportement doit intervenir dynamiquement, en fonction de cet état.
- Les opérations comportent des déclarations conditionnelles fonctions de l’état de l’objet. Dans ce cas, on place chaque branche de la condition dans une classe concrète séparée. L’état de l’objet est traité comme un objet.
- Si les états n’ont pas de données intrinsèques ( données propres à chaque objet état), on peut définir un état comme un singleton. Le constructeur sera privé et on y accèdera grâce à une méthode de fabrication statique ``getInstance()``.

**Exemple :**

On souhaite créer un distributeur de bonbons qui fonctionne de la manière suivante:

- Pour obtenir un bonbon, il faut insérer une pièce puis tourner la poignée pour obtenir le bonbon ou appuyer sur le bouton annuler pour récupérer la pièce.
- S’il n’y a plus de bonbons dans le distributeur, la pièce est éjectée.
- Une fois le bonbon délivré, s’il y a encore des bonbons, le distributeur est de nouveau en attente d’une pièce et s’il n’y a plus de bonbons dans le distributeur, il est en attente d’être rechargé.


### Pattern Itérateur

**Objectif :**

- Parcourir les éléments d’une collection sans révéler sa structure interne. 
- On peut avoir plusieurs façons de parcourir la collection, chaque parcours étant dédié à un usage spécifique. 
- On peut vouloir gérer simultanément plusieurs parcours dans une même collection d’objets.


**Exemple 1 :**

- On veut proposer une structure arborescente qui puisse être utilisée dans différents contexte. On crée une classe *Arbre*. Il y a plusieurs parcours possibles : parcours en profondeur, en largeur, parcours symétrique... On ne peut pas définir les parcours dont le client aura besoin.

- Comment permettre d’ajouter de nouveaux parcours sans avoir à modifier la classe *Arbre*?

1. Extraire le comportement qui permet de parcourir l’arbre et le mettre dans un objet séparé qu’on appelle un **itérateur**.
2. Définir une interface *Iterateur* qui permet de visiter l’élément courant tant qu’il y a un élément à visiter qui sera implémentée par chaque itérateur
3. Ajouter à la classe *Arbre* une méthode ```public Iterateur creerIterateur()```

**Solution :**

- Extraire de la collection les fonctions en charge des accès et parcours pour les placer dans un objet **itérateur**.
- L’itérateur sait quels éléments ont déjà été parcourus et assure le suivi de l’élément courant.
- Le client n’a pas besoin de savoir comment les éléments sont stockés dans la collection ni comment l’itérateur est implémenté. Il ne connait qu’une interface Iterateur qui fournit les services permettant de parcourir la collection.
![[Pasted image 20231002094837.png]]

![[Pasted image 20231002094848.png]]

**Interface** ```Iterable<T>```
```java
public inteface Iterable<T>{
	Iterator<T> iterator();
	default void forEach(Consumer<? Super T> action){
	/*...*/}
}
```
**Interface** ``Iterator``
```java
public Interface Iterator<E>{
	public boolean hasNext();
	public E next();
	public void remove();
}
```

**Exemple 2 :**

- On souhaite créer un outil d’envoi de spams vers les contacts d’utilisateurs de différents réseaux sociaux.
- Pour un profil donné, on souhaite accéder à ses amis pour leur envoyer certains messages mais aussi accéder à ses collègues pour envoyer d’autres types de messages. Les messages devront contenir le nom du contact.
- Pour créer un profil, on fournit le mail et le nom de la personne ainsi qu’une liste de contacts:

Exemple : "anna.smith@bing.com", "Anna Smith", "friend:mad_max@ya.com","friend:catwoman@yahoo.com ", "coworker:sam@amazon.com“.

```java
public class Profil{
	private String nom;
	private String email;
	private Map<String List<String>> contacts = new HashMap<>;
}
```
![[Pasted image 20231002095315.png]]

### Pattern Chaîne de responsabilités

**Objectif :**

- Eviter le couplage de l’émetteur d’une requête à ses gestionnaires, en donnant à plus d’un objet la possibilité de traiter la requête
- Chaîner les objets gestionnaires et faire passer la requête tout eu long de la chaîne, jusqu’à ce qu’un objet la traite.
- L’objet qui a émis la requête ne sait pas quel objet la traitera.

**Exemple :**

- Considérons un service d’aide contextuel proposé par une interface graphique. L’utilisateur peut obtenir de l’aide en cliquant sur n’importe qu’elle région de l’interface. L’aide fournie dépend de la partie choisie et de son contexte.
- Un bouton se trouve dans un panneau lui-même contenu dans la fenêtre.
- Si on clique sur le bouton et s’il n’y a pas d’aide prévue pour ce bouton, la demande d’aide va remonter au panneau qui affichera l’aide s’il y a une aide prévue sinon la demande va remonter à la fenêtre.

![[Pasted image 20231002095516.png]]

**Solution :**

- Chaque gestionnaire stocke une référence vers le prochain gestionnaire de la chaîne dans l’un de ses attributs.
- Il y a deux situations possibles :
	1. Chaque gestionnaire traite la demande et la fait passer plus loin dans la chaîne. La demande fait le tour de la chaîne jusqu’à ce que tous les gestionnaires aient eu l’occasion de la traiter
	2. Dès que la demande arrive à un des gestionnaires qui peut la traiter, il ne l’envoie pas plus loin dans la chaîne.

![[Pasted image 20231002095559.png]]

**Utilisation :**

- Utilisez la chaîne de responsabilité quand le programme doit traiter des types de demandes variées de différentes manières, mais que leur type exact et leur ordre dans la chaîne ne sont pas connus à l’avance.
- Utilisez ce patron si les gestionnaires doivent absolument respecter un ordre donné.
- Utilisez la chaîne de responsabilité si l’ensemble des gestionnaires et leur ordre dans la chaîne peuvent changer lors de l’exécution

### Pattern Visiteur

**Objectif :** 

- Effectuer des opérations sur les objets d’une structure en séparant les algorithmes et les objets sur lesquels ils opèrent

**Utilisation :**

- Une structure d’objets contient beaucoup de classes différentes d’interfaces distinctes et on veut réaliser des opérations sur ces objets qui dépendent de leur classe concrète mais
	1. sans pouvoir modifier les classes existantes
	2. Ou sans vouloir modifier les classes existantes car les opérations n’ont pas de relation entre elles et n’ont pas de lien avec l’interface des classes existantes
	3. Ou parce qu’on veut permettre l’ajout de nouvelles opérations en respectant le principe ouvert/fermé.

**Solution :**

- Créer une interface *Visiteur* contenant une opération *visite* pour chaque classe concrète de la structure d’objets
- Grouper toutes les opérations du même type dans une seule classe concrète qui implémente l’interface Visiteur.
- Faire en sorte que les objets de la structure « acceptent » un visiteur et lui indiquent la méthode à exécuter (technique de la double répartition)

![[Pasted image 20231002095751.png]]

**Exemple :**

- Considérons un compilateur qui présente les programmes sous forme d’arbre syntaxique. Il doit effectuer, sur ces arbres, des opérations telles que :
	- impression formatée
	- évaluation la profondeur du programme
	- des traitements d’analyse de sémantique
	- des restructurations de programme
- Selon la grammaire fournie, un programme sera composé d’une suite d’instructions, les instructions seront de type affectation ou print ou un bloc d’instructions.

```java
grammar grammaire;
//lexèmes
Id : [a-zA-Z]+[a-zA-Z0-9]*;
Int : [0-9]+;
//régles
exp :
	Id    #expId
	|Int  #expInt
	|exp op=('+'|'-'|'*'|'/') exp #expBinop
	|op=('cos'|'sin') exp #expUnop
;
instruction :
Id '=' exp ';' #instAffectation
| 'print' '(' exp ')'';' #instPrint
| 'block' '{'
		instruction*
		'}‘ #instBlock;

programme : instruction*;
//
```

**Exemple de programme :**

```python
x = 4;
print(2 + x);
block {
	   y = x;
	   z = 3*7;
	   block{
	   c = cos(x);
	   s = sin(10);
	   }
}
```

![[Pasted image 20231002100245.png]]

