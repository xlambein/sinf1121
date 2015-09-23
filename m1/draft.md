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
