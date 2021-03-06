Question 1
----------

Un type abstrait de données est une façon de concevoir un type de données en informatique, dans laquelle le type est défini du point de vue de l'utilisateur, à travers ses valeurs possibles et les opérations que l'on peut effectuer dessus, par opposition à un type défini à travers son implémentation[[1]][adtwiki].

À partir de cette définition, il est relativement évident de voir que la façon de décrire un TAD en Java est en utilisant une interface : en effet, celles-ci fournissent *uniquement* une liste des opérations possibles sur le type, sans aucune implémentation.


Question 2
----------

Pour implémenter `push()`, il faut parcourir toute la liste afin de récupérer le dernier noeud, puis créer un nouveau noeud et changer le pointeur du dernier noeud vers celui-ci.

```java
if (first == null)
    first = theNewNode;
else
{
    node = first;
    while (node.next != null)
        node = node.next;
    node.next = theNewNode;
}
```

Pour implémenter `pop()`, il faut parcourir toute la liste afin de récupérer l'avant-dernier noeud et le dernier noeud, récupérer la valeur du dernier noeud et mettre le pointeur de l'avant-dernier à null.

```java
if (first == null)
    return null;
else
{
    node = first;
    prev = null;
    while (node.next != null)
    {
        prev = node;
        node = node.next;
    }
    if (prev == null)
        first = null;
    else
        prev.next = null;
    return node;
}
```

Cette solution est bien moins efficace que si l'on faisait les opérations en début de liste : en effet, ici `push()` et `pop()` s'effectuent en O(n), tandis que si ces opérations se faisaient en début de liste, le temps serait constant.

Question 3
-----------
La classe Stack gere une pile en LIFO (le dernier objet à rentrer est donc le premier à partir). Elle possède 5 méthodes : push(E item), pop(), empty(), peek() et search(Object o). empty() sert à savoir si la pile est vide. peek() permet de savoir quel est l'objet du dessus de la pile mais sans l'enlever. search(Object o) regarde si l'argument est dans la pile et retourne sa position dans le cas échéant.
Question 4
-----------
On peut remplir juste une file avec push qui rajoute un élément. Lorsque la méthode pop est utilisée on vide la première file dans la deuxième à l'exception du dernier élément que l'on récupère. Si on empilé 1 2 3 sur la pile, une des deux files sera donc vide et l'autre contiendra 1 2 3. Si on utilise pop, on retire de façon classique le dernier élément arrivé dans la pile (ici, 3) et on le place dans la file qui était vide. On agit de la même manière pour le 2. L'élément que l'on voulait retirer (le 1) est alors accessible. La complexité de pop sera alors de 2N-1.
Question 5
-----------
Ci-dessous ce trouve les deux codes en JAVA pour écrire un string dans un fichier ou lire une seul ligne d'un fichier.
```java
/**
     *  Generic and primitive methods to write into a file
     * 
     * @pre  - a String of your choice and a destination file name
     * @post - Write the string from "word" into the file with the name from "file"
     *         When an IO Exception occurred, the methods shut himself down.
     */
	public static void Write(String word,String file){
		try{
			BufferedWriter bWrite = new BufferedWriter(new FileWriter(file));
			bWrite.write(word);
			bWrite.close();
		}catch(IOException e){
			System.exit(-1);
		}
	}
	
```
```java
    /**
     *  Generic and primitive methods to read a single line from a file
     * 
     * @pre  - a file name
     * @post - Return a string creating from the first line written in the file
     *         When an IO Exception occurred, the methods shut himself down
     *         When the file name or the fil himself is invalid, the methods return null.
     */
	public static String Read(String file){
		String word = null;
		try{
			BufferedReader bRead = new BufferedReader(new FileReader(file));
			word = bRead.readLine();
			bRead.close();
		}catch(FileNotFoundException e0){ return null; 
		}catch(IOException e1){ System.exit(-1);
		}
		return word;
	}
```

Question 6
-----------
 En utilisant le DOS, il est possible de faire appel à un programme JAVA et de lui faire passer des arguments. Ces derniers seront reçu par le programme dans le tableau initiale d'arguments: "String args[]". Ainsi, selon ce programme banale:
```java
 public static mainBanale(String args[]){
    System.println(args[0]);
    System.println(args[1]);
 }
```
 De ce fait, lors de l'exécution du programme via le DOS. 
```java
    mainBanale Un Deux
```
 Nous lirons dans la console:
```java
 Un
 Deux
 ```
 
 Question 7
----------
Le paramètre -Xmx définit la taille maximale de mémoire qu'on peut allouer sur le tas.
Par contre, le drapeau -Xms spécifie la taille de la mémoire initiale du tas.
Si on met une valeur très faible au paramètre -xmx, il se peut que le programme risque de ne pas avoir assez de mémoire car il aura atteint la taille maximale du tas.
Par contre, le paramètre -Xms peut accélérer le programme, ça peut éviter au programme d'agrandir le tas constamment. Ce qui améliore un peu les performances.

Question 8
----------
Un itérateur est un objet qui permet de parcourir tous les éléments de, par exemple, une liste.
Utiliser un itérateur est utile, cela permet d'explorer tous les objets d'une liste.
Si on modifie la structure de données alors qu'on est en train d'itérer sur celle-ci, il est possible qu'on arrive à un problème. Si jamais on supprime un noeud alors qu'un itérateur pointe sur ce noeud, l'itérateur ne pointera plus sur un objet mais vers null. Il ne sera donc plus possible de parcourir la liste.

Si le client modifie la collection avec un push() ou un pop() durant l'itération, il faut modifier le code de l'itérateur du Stack qui lance une java.util.ConcurrentModificationException. Pour se faire, il faut maintenir un compteur qui compte le nombre de push() et de pop() réalisés. Quand on crée l'itérateur, il faut stocker le compteur comme une variable dans l'instance de l'itérateur. Avant d'appeler hasNext() ou next(), il faut chaque fois vérifier si cette valeur n'a pas changé. Si elle a changé, une exception java.util.ConcurrentModificationException sera lancée.

Si on ne désire pas utiliser la fonctionnalité remove(), c'est une bonne idée de la laisser vide. On est obligé d'avoir une méthode remove() car elle est déclarée dans l'interface. On la laisse vide puisqu'on ne veut pas l'utiliser. Si jamais on appelle cette fonction, rien ne se passera.


Question 9
----------
Pour comprendre le besoin d'une notation différente, il faut comprendre les avantages limitations des autres.

Les trois notations les plus connues sont big Oh, big Theta, et big Omega. Elles ont chacune leurs intérêt et limitations.

Big Oh comporte l'ensemble des fonctions qui grandissent asymptotiquement plus vite que la fonction étudiée.

Soit g(x) une fonction faisant correspondre le nombre d'instruction à la taille du problème (x).

f(x) ∈ O(g(x)) veut dire que f(x) grandira asymptotyquement plus vite que g(x). Il existe donc une infinité de fonction appartenant à O(g(x)), celles qui grandissent asymptotiquement aussi vite que g(x), et toutes celles qui grandissent asymptotiquement plus vite. Big Oh est intéressant lorsque ce qui nous intéresse est le pire des cas.

Big Omega d'une fonction est l'opposée: l'ensemble des fonction qui grandissent asymptotiquement moins vite que la fonction, c'est rarement intéressant à savoir car on cherche généralement à savoir si un algorithme est plus rapide qu'un certain seuil, et rarement s'il est plus lent (on s'intéresse rarement au meilleur des cas).

Big Theta d'une fonction est déjà beaucoup plus précis: l'ensemble est restreint aux fonction du même ordre, ce qui corresponds aux fonctions qui grandissent asymptotiquement à une vitesse équivalente, avec une variation d'au plus une constante multiplicative.

Par exemple:

si

f(x) ∈ Θ(g(x))

alors

2f(x) ∈ Θ(g(x))

mais pas 

f(x)² ∈ Θ(g(x))

La notation en tilde est encore plus précise, les fonctions doivent grandir asymptotiquement de la même manière.

Mathématiquement, cela donne:

on dit que g(x) ~ f(x) si et seulement si:

lim(x → ∞) g(x)/f(x) = 1.

Pour résumer, la notation en tilde est plus précise que les trois autres, car elle met une limite inférieure ET une limite supérieure, de plus elle est plus restreinte que la notation Theta dont la précision s'arrête à l'ordre.

Question 10
----------

Pour effectuer le test du "doubling ratio", il suffit de tester le runtime en fonction de la taille du problème, et de doubler la taille du problème entre chaque test.
Les problème de ce type de test sont qu'il faut que le "growth ratio" (nous verrons plus bas ce dont il s'aggit) atteigne une valeur limite et qu'il n'est pas possible de tester au delà d'une certaine taille de problème (parce qu'on double la taille du problème à chaque fois, on atteint rapidement des tailles astronomiques), l'avantage c'est qu'il donne quand même des données intéressante et souvent suffisantes pour déduire la caractérisation de l'implémentation et prévoire des runtimes avec une plus grosse taille de problème.

À partir du test du doubling ratio, on peut extraire le "growth ratio", au ratio d'augmentation du runtime quand la taille des données double. Dans le cas présenté il est impossible de l'obtenir entre une taille de problème de 2000 et 4000 car le runtime est trop petit (il a même été arrondi à 0).

Le calcul pour obtenir le ratio est runtime/(runtime Précedent).

Nous obtenons ainsi les valeurs 3 (de 4000 à 8000), 4.3 (de 8000 à 16000), 3.92 (de 16000 à 32000) et de 4.0 (de 32000 à 64000).

Le "growth ratio" semble osciller autours de 4 lorsque la taille du problème est assez grande, nous estimerons que la valeur limite est de 4, bien que plus de données auraient permis de confirmer sa vraie valeur.

À partir de ce "growth ratio" que nous estimons à 4, nous allons chercher la caractérisation de l'algorithme.

Pour cela nous utiliseront les formules:

T(N) = a*N^b

et

"growth ratio" = 2^b

où N est la taille du problème, T(N) est le runtime en fonction de la taille du problème et "a" et "b" sont des constantes.

Pour caractériser T(N) correctement, il nous faut trouver "a" et "b"

Commençons par b, on sait:

"growth ratio" = 2^b

donc

log(2, "growth ratio") = b

Nous avons estimé le "growth ratio" à 4, cela nous donne:

b = 2

trouvons maintenant a:

utilisons un runtime connu (par exemple pour N = 64000, T(N) = 20.5)

20.5 = a*64000^2

on peut isoler a:

20.5/(64000^2) = a

on obtient:

a = 5*10^-9

donc

T(N) = (5*10^(-9))*(N^2)

pour N = 128000 ça fait T(128000) = 81,92.


Question 11
-----------

Un bon ensemble de tests unitaires devrait, pour chaque opération, couvrir les cas normaux --- c'est-à-dire, les arguments et valeurs internes de la structure à l'intérieur de leur domaines ---, les cas limites --- aux bords du domaine ou à l'infini --- et les erreurs --- hors du domaine. Par exemple, dans le cas d'une pile, la méthode `pop()` devrait être testée avec quelques éléments dans la pile (cas normal), avec un seul élément et avec un grand nombre d'éléments (cas limites) et avec zéro éléments (erreur car hors du domaine)[[2]][gooddstests].

La génération de données aléatoires pour les tests permet de trouver des cas limites supplémentaires (cette technique s'appelle le *fuzz testing* ou *fuzzing*)[[3]][fuzztesting]. L'usage d'un seed fixé est important afin d'être en mesure de reproduire les mêmes bugs à chaque test.

Un outil d'analyse de couverture de code permet de vérifier que chaque partie du code source (c'est-à-dire: fonctions, instructions, etc) a été exécutée lors des tests, et donc de savoir si certaines sections du programmes ne sont pas couvertes par les tests existant[[4]][codecoverage].

Pour vérifier expérimentalement la complexité temporelle, il suffit de lancer des tests avec des données aléatoires de taille `n` différentes (par exemple, 10^1, 10^2, 10^3, ...), et de voir si le temps d'exécution évolue bien de la manière décrite par la complexité théorique lorsque `n` devient grand. Si par exemple entre deux ordres de grandeur le temps d'exécution est multiplié par 100, l'expérience montre que la complexité est quadratique.

[adtwiki]: https://en.wikipedia.org/wiki/Abstract_data_type
[gooddstests]: https://courses.cs.washington.edu/courses/cse373/05wi/slides/testingds-1.ppt
[fuzztesting]: https://en.wikipedia.org/wiki/Fuzz_testing
[codecoverage]: https://en.wikipedia.org/wiki/Code_coverage
