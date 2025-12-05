# TP Git : Manipulation des branches, commits, push, merge et résolution de conflits

Ce dépôt contient les exercices pratiques sur Git, incluant la création de branches, la fusion (merge) et la résolution de conflits.

## TP1 – Manipulation des branches, commits, push et fusion avec Git

### Objectif
Pratiquer les bases de Git : commits, branches, push et merge.

### Étapes réalisées

1. **Travail sur la branche `main`**
   - Création du fichier `code.py` avec le contenu initial :
     ```python
     from datetime import datetime
     print("Hello ! Il est {}.".format(datetime.now().strftime("%H:%M:%S")))
     ```
   - Ajout et commit :
     ```bash
     git add code.py
     git commit -m "Ajout du fichier code.py"
     ```
   - Affichage de l'historique : `git log`
   - Push sur GitHub : `git push origin main`

**Note :** Dans cette implémentation, les étapes suivantes ont été effectuées directement sur la branche `main`, sans création de la branche `refonte`. Cela signifie que la branche séparée n'a pas été utilisée pour isoler les modifications. Pour une organisation plus propre, il est recommandé de créer des branches pour les nouvelles fonctionnalités.

2. **Ajout du module** (directement sur `main`)
   - Création du fichier `module.py` :
     ```python
     from datetime import datetime

     def obtenir_temps():
         return "Hello ! Il est {}.".format(datetime.now().strftime("%H:%M:%S"))
     ```
   - Modification de `code.py` :
     ```python
     from module import obtenir_temps
     print(obtenir_temps())
     ```
   - Commit : `git commit -m "Ajout du module et mise à jour du code"`

**État actuel :** Les fichiers `module.py` et `code.py` (modifié) sont sur la branche `main`.

## TP2 – Création et résolution d’un conflit de merge avec Git

### Objectif
Provoquer un conflit de merge, l'observer et le résoudre.

### Étapes réalisées

1. **Vérifier l'état du dépôt** : `git status` - Dépôt propre.

**Note :** Un commit "Sauvegarde avant nettoyage" a été créé pour préparer.

2. **Créer la branche `conflit-a`**
   - `git checkout -b conflit-a`
   - Modification de `code.py` :
     ```python
     print("Version A du code")
     ```
   - Commit : `git commit -m "Modification version A"`

3. **Retour sur `main`** : `git checkout main`

4. **Créer la branche `conflit-b`**
   - `git checkout -b conflit-b`
   - Modification de `code.py` :
     ```python
     print("Version B du code")
     ```
   - Commit : `git commit -m "Modification version B"`

5. **Fusionner `conflit-a` dans `main`**
   - `git checkout main`
   - `git merge conflit-a` : Fusion sans conflit.

6. **Fusionner `conflit-b` dans `main`**
   - `git merge conflit-b`
   - **Conflit détecté :**
     ```
     Auto-merging code.py
     CONFLICT (content): Merge conflict in code.py
     Automatic merge failed; fix conflicts and then commit the result.
     ```

7. **Observer le conflit**
   - Ouvrir `code.py`, le conflit apparaît avec les marqueurs :
     ```
     <<<<<<< HEAD
     print("Version A du code")
     =======
     print("Version B du code")
     >>>>>>> conflit-b
     ```

   ![Image du conflit](conflict_screenshot.png)
   *Figure 1 : Capture d'écran du conflit dans code.py. Si l'image n'est pas présente, prend une capture d'écran lors de l'exécution de `git merge conflit-b`avant de résoudre le conflit.*

8. **Résoudre le conflit**
   - Choix d'une version finale :
     ```python
     print("Version finale du code après résolution du conflit")
     ```
   - Valider : `git add code.py` puis `git commit -m "Résolution du conflit entre conflit-a et conflit-b"`
   - Push : `git push origin main`

### Branches actuelles
- `main` : Branche principale avec les résolutions.
- `conflit-a` : Contient la version A.
- `conflit-b` : Contient la version B.

### Historique des commits
Voir `git log --oneline --graph --all` pour visualiser les fusions et branches.

## Instructions pour reproduire ou corriger

- Pour refaire le conflit : Supprimer les branches existantes si nécessaire et recommencer à l'étape 2 de TP2.
- Pour prendre une capture d'écran : Exécuter `git status` et ouvrir `code.py` en VS Code lors du conflit, capturer et nommer `conflict_screenshot.png`.

## Fichiers du projet
- `code.py` : Fichier principal (version finale après résolution).
- `module.py` : Module utilisé dans TP1.
