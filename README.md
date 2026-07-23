<p align="center"><img src="koseki-logo.png" alt="Koseki" width="560"></p>

# Koseki（戸籍）

*Koseki* — le registre familial japonais, tenu de génération en génération.

Application de généalogie **hors-ligne**, en un seul fichier HTML, sans dépendance ni serveur.
Importez un fichier GEDCOM, complétez votre arbre, visualisez les migrations de votre lignée —
tout reste sur votre appareil.

## Démarrage

Ouvrez simplement `index.html` dans un navigateur, ou déployez-le sur GitHub Pages :

1. Créez un dépôt `koseki` et poussez-y les fichiers. **Le fichier de l'application doit s'appeler
   `index.html`** : sans lui, GitHub Pages affiche le README à la place du site.
2. Settings → Pages → Source : *Deploy from a branch* → branche `main`, dossier `/ (root)`
3. Après une minute, l'application est en ligne à l'adresse `https://<utilisateur>.github.io/koseki/`

> Deux adresses à ne pas confondre :
> `github.com/<utilisateur>/koseki` est la page **du code** — elle affiche toujours le README, c'est normal.
> `<utilisateur>.github.io/koseki/` est l'**application** elle-même.

Les données restent locales (IndexedDB), rien n'est envoyé au serveur.

## Fonctionnalités

- **Import GEDCOM 5.5.1 sans perte** — les balises non gérées (sources, médias, balises propriétaires
  MyHeritage/Geneanet/Ancestry…) sont conservées telles quelles et restituées à l'export
- **Multi-projets** — plusieurs arbres indépendants sur le même appareil
- **Édition complète** — état civil, événements (naissance, baptême, décès, mariage, profession,
  résidence…), liens familiaux (parents, conjoints, enfants), création de personnes
- **Fiche individuelle** style acte d'état civil avec mentions marginales, imprimable
- **Arbre d'ascendance SVG** interactif (3 à 7 générations), navigation au clic, export SVG
- **Descendance** en arborescence dépliée
- **Carte des migrations** — voir ci-dessous
- **Tableau de bord** — statistiques, naissances par demi-siècle, patronymes et communes les plus
  fréquents, longévité moyenne
- **Contrôle qualité** — incohérences chronologiques (décès avant naissance, parent trop jeune ou trop
  âgé, naissance après décès du parent, longévité improbable), données manquantes, doublons probables
- **Recherche globale** insensible aux accents
- **Export** GEDCOM réimportable partout + sauvegarde/restauration JSON

## Carte des migrations

Une carte interactive retrace les déplacements de la lignée à travers les siècles, entièrement
hors-ligne : le fond de carte (monde + départements français) et le référentiel géographique sont
embarqués dans le fichier.

- **Deux types de mouvements**, activables séparément :
  - *filiations* — du lieu de naissance des parents à celui de leurs enfants (la dérive géographique
    d'une lignée au fil des générations)
  - *vies* — du lieu de naissance au lieu de décès d'une même personne
- **Curseur temporel et animation** : faire défiler les siècles et regarder la famille se déplacer,
  avec deux lectures possibles :
  - *cumulé* — tous les déplacements survenus jusqu'à la date affichée s'accumulent
  - *seulement les vivants à cette date* — les déplacements disparaissent à la mort des personnes
    concernées : on ne voit que les contemporains de l'année affichée, et les générations se
    renouvellent au fil de l'animation (à défaut de date de décès connue, une vie est estimée à 85 ans)
- **Légende illustrée** sous la carte, expliquant chaque couleur, l'épaisseur des traits, la taille
  des cercles et les positions approchées
- **Points ancrés** : chaque commune est un point de taille constante à l'écran, fixé à ses coordonnées.
  Il ne bouge ni ne change de taille quand on zoome — la taille traduit le nombre d'événements du lieu.
  Un appui liste les personnes concernées.
- **Étiquettes des communes** en surcouche, sans chevauchement : elles suivent le déplacement sans décalage
  et se densifient à mesure qu'on zoome
- **Zoom et déplacement** à la molette et au glisser ; vues France / Monde préréglées
- **Statistiques** : distance moyenne, plus grand déplacement, répartition par siècle

### Géocodage

Les lieux sont localisés hors-ligne à partir de leur libellé GEDCOM, par ordre de précision :
commune française exacte (référentiel de 35 923 communes embarqué), puis département, région et pays.
Sur un fichier de test réel de 2 376 personnes, **84 % des lieux sont résolus à la commune exacte**.

Les positions approchées sont signalées par un cercle en pointillés. Le panneau *Gérer les lieux*
permet de corriger n'importe quelle position à la main (latitude / longitude) ; la correction est
mémorisée dans le projet — utile notamment pour les lieux étrangers, que le référentiel ne couvre
qu'au niveau du pays.

## Importer son arbre

Quatre voies, au choix — utile car iOS grise parfois les fichiers `.ged` dans l'app Fichiers :

1. **Sélecteur de fichier** (aucune extension n'est filtrée)
2. **Glisser-déposer** sur la zone d'import (ordinateur)
3. **Copier-coller** du contenu du fichier, dans le panneau *Le fichier est grisé ?*
4. **Chargement depuis une adresse** — si le `.ged` est déposé dans le même dépôt que l'application,
   son nom seul suffit (ex. `cagnat_normalise.ged`)

Astuce iOS supplémentaire : renommer le fichier en `.txt` dans l'app Fichiers le rend sélectionnable.

Les fichiers encodés en Windows-1252 (ANSI) sont détectés et convertis automatiquement.

## Installer sur l'écran d'accueil

L'application est installable comme une application native, avec son icône :

- **iOS / iPadOS** — ouvrir le site dans Safari, bouton Partager → *Sur l'écran d'accueil*
- **Android** — Chrome, menu → *Installer l'application* (ou *Ajouter à l'écran d'accueil*)

Elle s'ouvre alors en plein écran, sans barre de navigateur. `manifest.webmanifest` et
`koseki-app-icon.png` doivent être présents à la racine du dépôt, à côté de `index.html`.

## Sur téléphone et tablette

L'application est utilisable au doigt sur Android et iOS :

- **Arbre et carte** — pincer pour zoomer, glisser pour se déplacer, double-appui pour zoomer d'un cran ;
  des boutons `+` / `−` sont également disponibles. Un appui simple sur une case recentre l'arbre,
  un double-appui ouvre la fiche.
- **Pas de zoom involontaire de la page** : le zoom du navigateur est neutralisé (y compris sur Safari iOS,
  qui ignore `user-scalable=no`), et les champs de saisie font 16 px pour éviter le zoom automatique d'iOS
  à la mise au point.
- Tableaux et en-tête s'adaptent aux écrans étroits, sans défilement horizontal.

## Note technique

Les épaisseurs de trait et les tailles de points sont recalculées en JavaScript à chaque
changement de vue plutôt que confiées à `vector-effect="non-scaling-stroke"` : cette propriété
n'est pas appliquée de la même façon par tous les navigateurs, ce qui donnait des points
démesurés sur Safari iOS. Le regroupement des tracés par style (une trentaine d'éléments SVG
pour plusieurs centaines de lieux) rend ce recalcul quasi gratuit.

## Confidentialité

Aucune donnée ne quitte le navigateur. La persistance utilise IndexedDB.
Pensez à exporter régulièrement une sauvegarde (GEDCOM ou JSON) : les données locales
peuvent être effacées si vous videz les données de navigation.

## Compatibilité

Navigateurs modernes (Chrome, Edge, Firefox, Safari), ordinateur et mobile.
Testé avec des exports MyHeritage (2 376 individus), y compris leurs particularités
non conformes (notes multilignes, balises propriétaires).

## Crédits des données

- Fond de carte mondial et contours des départements français : données publiques
  (Natural Earth / découpage administratif français), simplifiées pour l'embarquement.
- Référentiel des communes françaises (nom, département, coordonnées) : données publiques
  issues du fichier officiel des codes postaux et communes.
