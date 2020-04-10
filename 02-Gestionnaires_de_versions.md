# Chapitre 2. Gestionnaire de versions

## 2.1. CVS

(*Current Version System*)

## 2.2. Subversion

*Amélioration de CVS*.

## 2.3. Mercurial

Similaire à *git*

## 2.4. git

Créé en 2005 par Linus Torvald.

Chaque fichier peut se trouver dans une ou plusieurs des 3 zones suivantes:

- *Zone courante*: contenu actuel de chaque fichier.

- *Zone de transit* (*staging area*): fichiers après ajout (`add`) mais avant soumission (`commit`).

- *Dépôt*: fichier après soumission (`commit`).

### 2.4.1. Configuration

Depuis la ligne de commande:

- Coloration lors de l'affichage des différences:

```bash
$ git config --global color.ui auto
```

- Éditeur par défaut:

```bash
$ git config --global core.editor "/usr/bin/emacs"
```

- ?:

```bash
$ git config --global push.default upstream
$ git config --global merge.conflictstyle diff3
```

- Définir l'adresse e-mail:

```bash
$ git config --global user.email "you@example.com"
```

- Définir le nom d'utilisateur:

```bash
$ git config --global user.name "Your Name"
```

- Activer le *credential helper*:

```bash
$ git config --global credential.helper cache
```

> et pour changer le *timeout* (à 1h):
> 
> ```bash
> $ git config --global credential.helper 'cache --timeout=3600'
> ```

Les mêmes commandes, sans l'option `--global`, n'affectent que la configuration du dépôt courant.

### 2.4.2. Dépôt local

![Zones](img/02-local_repository.png)

- Créer un nouveau dépôt local dans le répertoire courant:

```bash
$ git init
```

- Ajouter un fichier dans la zone de transit (*staging area*):

```bash
$ git add chemin/vers/fichier
```

> Il peut s'agir soit d'un nouveau fichier, soit d'un fichier existant mais modifié depuis.

- Enlever un fichier de la zone de transit:

```bash
$ git rm --cached chemin/vers/fichier
```

> Pour le supprimer en même temps:
> 
> ```bash
> $ git rm -f chemin/vers/fichier
> ```

- Soumettre le contenu de la zone de transit vers le dépôt (il s'ensuit l'ouverture automatique de l'éditeur par défaut):

```bash
$ git commit
```

> Chaque soumission se voit attribuée un nombre aléatoire entier sur 20 octets représenté sous la forme de 40 chiffres hexadécimaux.

### 2.4.3. Branche

Chaque branche est associée à un **label**. Celui par défaut s'appelle `master`. 

- Pour connaître la branche courante:

```bash
$ git branch
```

> Pour visualiser les branche distantes:
> 
> ```bash
> $ git branch -a
> ```

- Pour créer une nouvelle branche:

```bash
$ git branch <nouveau_label>
```

> -  Pour se placer sur cette nouvelle branche:
>   
>   ```bash
>   $ git checkout <nouveau_label>
>   ```
> 
> - Pour effectuer les 2 opérations en une seule commande:
>   
>   ```bash
>   $ git checkout -b <nouveau_label>
>   ```

- Pour supprimer une branche (uniquement son *label* mais pas les soumissions associées):

```bash
$ git branch -d <label>
```

- Pour visualiser graphiquement les soumissions entre 2 branches:

```bash
$ git log --graph --oneline master <autre_branche>
```

- Pour fusionner une branche (ici `branche2`) dans une autre (ici `branche1`):

```bash
$ git checkout branche1
$ git merge branche2
```

>  Dans le cas où des conflits apparaissent:
> 
> - éditer les fichiers, résoudre les conflits et supprimer les marquages spécifiques.
> 
> - pour annuler une fusion:
>   
>   ```bash
>   $ git merge --abort
>   ```

### 2.4.4. Consultation

- Connaître le numéro de version de `git`:

```bash
$ git --version
```

- Liste tout l'historique (décroissant) des soumissions d'une branche:

```bash
$ git log
```
