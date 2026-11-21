# Système de sauvegarde de l'architecture des données, fichiers et dossiers

![Arbores Restore logo](assets/branding/arbores-restore-logo.png)

Le logo officiel du projet est inclus dans `assets/branding/` en PNG carré et en ICO multi-résolution. L’ICO est configuré pour l’exécutable Python et l’application Windows Visual Basic.


**Reconstruire la structure. Pas les données.**

Cet outil recrée une arborescence de dossiers et des fichiers vides à partir d'un inventaire CSV. Il ne restaure pas le contenu des fichiers perdus.


## Pourquoi ce projet existe

J'ai perdu plus d'un téraoctet de données. Au-delà des fichiers, j'avais perdu l'organisation qui leur donnait du sens : les noms, les dossiers, les chemins et la manière dont mes projets étaient rangés. Je voulais retrouver au moins cette architecture lorsque les données elles-mêmes n'étaient plus récupérables.

Le projet utilise un inventaire CSV exporté de WizTree comme trace de l'ancien disque. Il vise à reconstruire cette structure ailleurs, pour pouvoir la parcourir et s'en servir comme repère dans de futures recherches ou tentatives de récupération.

## Ce que le logiciel fait

- Reconstruit des dossiers à partir des chemins de l'inventaire.
- Crée des fichiers vides (0 octet) portant les noms enregistrés.
- Permet une prévisualisation avant toute création.
- Filtre les fichiers/dossiers cachés et les entrées système selon les données disponibles.
- Filtre par extensions incluses/exclues et par noms de dossiers exclus.
- Signale les collisions, les chemins invalides et les entrées ignorées.
- Comprend une CLI Python, une version PowerShell et une interface Windows en Visual Basic.

## Ce que le logiciel ne fait pas

- Ne restaure pas les données binaires d'origine.
- Ne garantit pas une reconstruction parfaite avec un CSV incomplet, incompatible ou endommagé.
- Ne reconstitue pas des métadonnées qui ne figurent pas dans l'inventaire.
- N'écrase pas volontairement les éléments déjà présents.

Les tailles originales et les filtres basés sur la taille sont prévus pour une version ultérieure.

## Statut

Version de développement initiale `0.1.0`. La compatibilité est testée sur les exemples fournis, mais pas encore validée avec toutes les variantes de CSV WizTree. Avant utilisation réelle, testez avec un export anonymisé et choisissez un dossier de destination neuf sur un disque sain.

## Démarrage rapide

Python 3.10 ou plus récent :

```powershell
cd src/python
python -m pip install .
arbores-restore "C:\Inventaire\wiztree.csv" "E:\Arborescence_reconstruite" --preview
```

Après avoir vérifié la prévisualisation, relancez avec `--apply` pour créer les dossiers et fichiers vides. La CLI Python ne demande pas de confirmation interactive.

```powershell
arbores-restore "C:\Inventaire\wiztree.csv" "E:\Arborescence_reconstruite" --apply
```

## Tests

```powershell
cd src/python
python -m pip install -e . pytest
python -m pytest ../../tests -v
```

## Documentation

- [Origine](docs/origin-story.md)
- [Fonctionnement](docs/how-it-works.md)
- [Limites](docs/limitations.md)
- [Sécurité](docs/safety.md)
- [Guide WizTree](docs/guides/wiztree/README.md)
- [Contribuer](CONTRIBUTING.md)
- [Sécurité et signalement](SECURITY.md)

## État et feuille de route

Consultez [la feuille de route](docs/roadmap.md). Les analyses de popularité GitHub (étoiles, forks, téléchargements, trafic, évolution) seront suivies avec des données réelles une fois le dépôt publié ; ce suivi reste distinct de la fonction de reconstruction.
