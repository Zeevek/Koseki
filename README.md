<p align="center"><img src="koseki-logo.png" alt="Koseki" width="560"></p>

# Koseki（戸籍）

*Koseki* — le registre familial japonais, tenu de génération en génération.

Application de généalogie **hors-ligne**, en un seul fichier HTML, sans dépendance ni serveur.
Importez un fichier GEDCOM, complétez votre arbre, visualisez les migrations de votre lignée —
tout reste sur votre appareil.

## Démarrage

Ouvrez simplement `koseki.html` dans un navigateur, ou déployez-le sur GitHub Pages :

1. Créez un dépôt `koseki` et ajoutez `koseki.html` (renommez-le `index.html` pour avoir l'URL courte)
2. Settings → Pages → Deploy from branch → `main`
3. L'application est en ligne ; les données restent locales (IndexedDB), rien n'est envoyé au serveur

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
- **Curseur temporel et animation** : faire défiler les siècles et regarder la famille se déplacer
- **Points proportionnels** au nombre d'événements par lieu ; clic pour lister les personnes concernées
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
