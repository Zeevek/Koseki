<p align="center"><img src="koseki-logo.png" alt="Koseki" width="560"></p>

# Koseki（戸籍）

*Koseki* — le registre familial japonais, tenu de génération en génération.

Application de généalogie **hors-ligne**, en un seul fichier HTML, sans dépendance ni serveur.
Importez un fichier GEDCOM, complétez votre arbre, dépouillez des registres, cartographiez les
migrations de votre lignée — tout reste sur votre appareil, et tout ressort en GEDCOM standard.

## Démarrage

Ouvrez `index.html` dans un navigateur, ou déployez sur GitHub Pages :

1. Poussez les fichiers dans un dépôt. **Le fichier de l'application doit s'appeler `index.html`** :
   sans lui, GitHub Pages affiche le README à la place du site.
2. Settings → Pages → Source : *Deploy from a branch* → branche `main`, dossier `/ (root)`
3. L'application est en ligne à `https://<utilisateur>.github.io/koseki/`

> `github.com/<utilisateur>/koseki` est la page **du code** — elle affiche toujours le README.
> `<utilisateur>.github.io/koseki/` est l'**application**.

## Les vues

| Vue | Ce qu'elle apporte |
|---|---|
| **Tableau de bord** | Statistiques d'ensemble, naissances par demi-siècle, patronymes et communes |
| **Personnes** | Liste filtrable et triable de tout le registre |
| **Fiche** | Acte d'état civil avec mentions marginales, événements, sources, documents, livret imprimable |
| **Arbre** | Ascendance graphique 3 à 7 générations, zoomable, exportable en SVG |
| **Éventail** | Ascendance en éventail jusqu'à 9 générations d'un seul coup d'œil |
| **Descendance** | Arborescence dépliée de la postérité |
| **Sosas** | Liste numérotée Sosa-Stradonitz par génération, avec repérage des implexes |
| **Frise** | Chronologie d'une vie, replacée parmi ses contemporains |
| **Parenté** | Calcul du lien entre deux personnes via leur ancêtre commun |
| **Carte** | Migrations de la lignée à travers les siècles, animées dans le temps |
| **Sources** | Registres, actes, cotes d'archives, liens vers les vues numérisées, documents joints |
| **Statistiques** | Longévité, mortalité infantile, âge au mariage, fécondité, prénoms, métiers, endogamie |
| **Recherche** | Front de recherche : ancêtres à filiation incomplète, liens vers les bases externes |
| **Doublons** | Rapprochements probables et assistant de fusion champ par champ |
| **Lieux** | Renommer, fusionner et positionner les lieux du registre |
| **Saisie** | Dépouillement de registres en série : naissances, mariages, décès |
| **Qualité** | Incohérences chronologiques, données manquantes, doublons |
| **Données** | Import, export GEDCOM, sauvegardes, projets multiples |

## Sources et actes

Les sources sont des enregistrements GEDCOM standard, donc réimportables partout. Chacune porte
un titre, un auteur, un dépôt, une cote et **un lien vers l'acte numérisé**. Une source se cite
sur une personne ou sur un événement précis, avec la page ou la vue, et un niveau de fiabilité.

Des documents peuvent être joints : soit par lien externe, soit par image conservée dans
l'application (elle reste sur l'appareil et figure dans la sauvegarde JSON).

## Dépouillement de registres

L'onglet *Saisie* est prévu pour transcrire un registre du début à la fin. On fixe une fois le
contexte — source, commune, année, vue — puis on enchaîne les actes : chaque formulaire ne demande
que ce qui change. Les personnes déjà présentes sont proposées à la frappe, les nouvelles sont
créées à la volée, les familles se constituent automatiquement, et la source est citée sur chaque
acte enregistré. Un âge au décès crée une date de naissance estimée.

## Carte des migrations

- **Filiations** (naissance des parents → des enfants) et **vies** (naissance → décès), séparément
- **Curseur temporel** avec deux lectures : *cumulé* ou *seulement les vivants à cette date*
- Géocodage hors-ligne : 35 923 communes françaises embarquées, puis départements, régions et pays
- Positions corrigeables à la main dans l'onglet *Lieux*

## Importer son arbre

Quatre voies — iOS grise parfois les fichiers `.ged` :

1. Sélecteur de fichier (aucune extension filtrée)
2. Glisser-déposer
3. Copier-coller du contenu
4. Chargement depuis une adresse (le nom seul suffit si le fichier est dans le même dépôt)

Les fichiers encodés en Windows-1252 sont détectés et convertis automatiquement.

## Installer sur l'écran d'accueil

- **iOS / iPadOS** — Safari, Partager → *Sur l'écran d'accueil*
- **Android** — Chrome, menu → *Installer l'application*

`manifest.webmanifest` et `koseki-app-icon.png` doivent être à la racine, à côté de `index.html`.

> Sur iOS, une application installée dispose d'un stockage **séparé** de Safari : il faut y
> réimporter le GEDCOM une première fois.

## Confidentialité

Aucune donnée ne quitte le navigateur. Persistance en IndexedDB.
Exportez régulièrement une sauvegarde : vider les données de navigation efface tout.

## Notes techniques

- **Import GEDCOM 5.5.1 sans perte** : les balises non gérées (sources propriétaires MyHeritage,
  médias, notes malformées) sont conservées telles quelles et restituées à l'export.
- **Annuler / rétablir** sur 20 étapes (Ctrl+Z / Ctrl+Maj+Z), chaque étape mémorisant l'état complet.
- Le registre porte un numéro de version qui invalide les caches : contrôle qualité, géocodage,
  mouvements de la carte.
- Les épaisseurs de trait sont recalculées en JavaScript plutôt que confiées à
  `vector-effect="non-scaling-stroke"`, que Safari n'applique pas de la même façon.

## Crédits des données

Fond de carte mondial et contours des départements : données publiques (Natural Earth, découpage
administratif français). Référentiel des communes : fichier officiel des codes postaux.
