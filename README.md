# GITHUB-PAGE

# GNU/LINUX : Compiler un programme depuis les sources

Rédigé à partir d'un cours sur OpenClassroom : [article](https://openclassrooms.com/fr/courses/43538-reprenez-le-controle-a-laide-de-linux/42370-compiler-un-programme-depuis-les-sources "Compiler un programme depuis les sources")

https://openclassrooms.com/fr/courses/43538-reprenez-le-controle-a-laide-de-linux/42370-compiler-un-programme-depuis-les-sources

Trois solutions pour installer un programme sous LINUX :

1. **Dépôts offciels :** habituellement, les programmes sont disponibles dans des dépôts et installables via apt-get.
2. **Paquetage :** quand le programme n'existe pas on peut trouver un paquetage spécifique à une distribution (.deb pour Debian, .rpm pour RedHat)
3. **Sources :** quand le pquetage n'existe pas il faud compiler les sources 

## 1 - A partir des dépôts

Chercher le programme : `apt list <nom-programme>`
Si il existe installer le programme : `sudo apt install <nom-programme>`
Si le programme a des dépendances à installer, le terminal pour invitera à les installer.

## 2 - A partir d'un paquetage

Pour Debian ou Ubuntu, télécharger le fichier .deb et double-cliquer dessus.
Apparemment cette solution ne règle pas le problème des dépendances.

## 3 - A partir des sources

Télécharger le fichier source qui aura une archive compressée avec l'extension `.tar.gz`

Extraire l'archive : `tar zxvf htop-0.8.3.tar.gz`

```
    ./configure
    make
    sudo make install
```

Après le `./configure` il peut y avoir des erreurs, notamment des problèmes de dépendance.

Il faut les régler avant de lancer le `make`et relancer ensuite le `./configure`.

# Exemples d'erreurs :

* **Extraction de l'archive : après le tar**

```
tar: This does not look like a tar archive
tar: Skipping to next header
tar: Exiting with failure status due to previous errors
```

`gzip -dc hello-0.2.tar.gz | tar -zxf -`

* **Après le `./configure`(ici pour installer **htop**)**

```configure: error: You may want to use --disable-unicode or install libncursesw```

Il faut chercher dans les dépôts de sa distribution, le paquet qui contient la librairie `libncursesw`.
Par exemple, sous Ubuntu, le paquet `apt-file` permet de chercher un nom de programme dans la liste des paquets des dépôts.
Donc dans un premier temps installer le paquet `apt-file` à partir des dépôts.
Puis faire `apt-file search libncursesw`

Et comme on souhaite compiler les sources d'un programme, il faut la version -dev de la lib.
Dans le cas de libncursesw prendre : `libncursesw5-dev: /usr/lib/x86_64-linux-gnu/libncursesw.a`

