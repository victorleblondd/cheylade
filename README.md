# Cheylade — proposition de nouveau site pour la commune

Proposition de nouveau site internet pour la commune de Cheylade (Cantal, 15400), sur le modèle du site de
[Saint-Bonnet-de-Condat](https://saint-bonnet-de-condat.fr/), publiée avec GitHub Pages :
https://victorleblondd.github.io/cheylade/

Le site officiel actuel de la commune reste [cheylade.fr](https://www.cheylade.fr). Tant que la mairie n'a pas
adopté la proposition (`proposition: true` dans `_config.yml`), chaque page affiche un bandeau « Proposition de
nouveau site », le site n'est pas référencé par les moteurs de recherche et les mentions légales sont au nom
de l'auteur de la proposition.

GitHub construit le site automatiquement (Jekyll) à chaque modification de la branche `main`.
Aucune installation n'est nécessaire.

## Sources des contenus

- Les avis de la mairie (affiches et textes, de juin à octobre 2026) et le journal communal *Cheylade & vous* n°2 (octobre 2026).
- Le site actuel de la commune (cheylade.fr) : délégations et commissions des élus, services, salle des fêtes, commerces et artisans.
- Le Répertoire national des élus (version du 11 août 2026) : le conseil municipal élu le 15 mars 2026.
- L'Insee (population légale 2023, répertoire Sirene pour les associations) et Wikipédia (géographie, histoire).
- La base Mérimée du ministère de la Culture : l'église Saint-Léger, le château d'Escorolles et l'oratoire du Sartre.
- La décision du 27 mars 2026 renouvelant le label Grand Site de France Puy Mary – Volcan du Cantal.
- Le Parc naturel régional des Volcans d'Auvergne (boucle du lac des Cascades) et l'office de tourisme Destination Haut Cantal (camping, hôtel, restaurant).
- Santé.fr (pharmacie), La Banque Postale (agence postale communale) et VigiEau (sécheresse, consulté le 14 octobre 2026).

## Ajouter un avis « Infos & Alertes »

1. Déposer le PDF dans le dossier `documents/infos-alertes/`, nommé `AAAA-MM-JJ-sujet-court.pdf`
   (sans accents ni espaces).
2. Ouvrir `_data/infos_alertes.yml` et copier le modèle (en tête du fichier) **tout en haut de la liste** :
   date, type (`alerte` ou `info`), thème, titre, résumé, nom du PDF.

L'avis apparaît alors sur la page Infos & Alertes et sur l'accueil ; son titre et son bouton ouvrent le PDF.
Une alerte récente s'affiche aussi en bandeau rouge sur l'accueil pendant 3 jours
(ou jusqu'à la date indiquée dans `bandeau_jusquau`).

**Affiche disponible en ligne (image ou PDF) :** au lieu de déposer le fichier, ajouter une ligne
`adresse  documents/infos-alertes/AAAA-MM-JJ-sujet.pdf` dans `outils/fichiers-a-recuperer.txt`.
GitHub télécharge le fichier, convertit une image en PDF A4 et l'ajoute au site
(`.github/workflows/recuperer-fichiers.yml`). Plusieurs images séparées par `|` donnent un PDF de plusieurs pages.

## Ajouter un rendez-vous à l'agenda

Ouvrir `_data/agenda.yml` et ajouter le rendez-vous à sa place, dans l'ordre chronologique : date, date de fin
(facultative), date affichée, titre, détail et lieu (facultatifs). Les six prochains rendez-vous s'affichent
sur l'accueil, tous sur la page Vie locale ; un rendez-vous passé disparaît tout seul le lendemain.

## Ajouter un article au bulletin municipal

Créer un fichier dans le dossier `_posts/`, nommé `AAAA-MM-JJ-titre-court.html`, sur le modèle des articles
existants (en-tête : titre, date, numéro du journal, catégorie, résumé ; puis le texte en HTML simple).
L'article apparaît sur la page Bulletin municipal (`/bulletin-municipal/titre-court/`) et, s'il est récent,
sur l'accueil.

## Ajouter un document à l'affichage légal

1. Déposer le PDF dans le dossier `documents/affichage-legal/`, nommé `AAAA-MM-JJ-sujet-court.pdf`
   (ou ajouter son adresse dans `outils/fichiers-a-recuperer.txt`).
2. Ouvrir `_data/affichage_legal.yml` et copier le modèle **en tête de la liste `documents`** :
   date de publication, type (`compte-rendu`, `deliberation`, `proces-verbal`, `convocation`,
   `arrete-municipal`, `arrete-prefectoral` ou `divers`), numéro (facultatif), titre, nom du PDF.

Les filtres par type et par année apparaissent dès le premier document. Les années proposées se règlent
dans le même fichier (`annees`) ; le filtre « Année » n'apparaît qu'à partir de deux années.

## Publier une version (Release)

Pour marquer une version importante, ajouter un fichier `outils/versions/vX.Y.Z.md`
(par exemple `v1.0.0.md`) : titre, commit marqué, puis les notes.
GitHub crée alors la Release correspondante (`.github/workflows/publier-version.yml`).

## Modifier les informations

| À modifier | Fichier |
|---|---|
| Adresse, téléphone, courriel, horaires de la mairie, page Facebook | `_data/mairie.yml` |
| Maire, adjoints, conseillers, délégués, commissions | `_data/elus.yml` |
| Rendez-vous | `_data/agenda.yml` |
| Menu principal | `_data/navigation.yml` |
| Bandeau d'annonce temporaire de l'accueil (texte, dernier jour d'affichage) | `_data/annonce.yml` |
| Encadrés « Sécheresse » (afficher ou masquer, niveau, arrêté) | `_data/secheresse.yml` |
| Pages | `mairie.html`, `vie-pratique.html`, `vie-locale.html`, `decouvrir.html`… |
| Apparence | `assets/css/site.css` (augmenter le numéro `?v=` dans `_includes/head.html` à chaque changement) |
| Proposition / site adopté par la commune | `_config.yml` (`proposition`, `site_officiel_actuel`) |

## Le jour où la mairie adopte le site

1. Dans `_config.yml`, passer `proposition` à `false` (le bandeau disparaît, le site devient référençable
   et les mentions légales passent au nom de la commune).
2. Avec un nom de domaine (par exemple cheylade.fr, aujourd'hui utilisé par le site actuel) : ajouter un
   fichier `CNAME` contenant le domaine, mettre `url` sur `https://le-domaine.fr` et `baseurl` sur `""`,
   puis configurer la zone DNS (comme pour Saint-Bonnet-de-Condat).

## Organisation

- `_layouts/` : gabarits communs (pages, articles du bulletin)
- `_includes/` : éléments réutilisés (avis, agenda, horaires, icônes, dates en français)
- `_posts/` : articles du bulletin municipal
- `assets/images/` : photo de l'église Saint-Léger et blason du Cantal
- `documents/infos-alertes/` : avis en PDF
- `documents/affichage-legal/` : documents de l'affichage légal en PDF

## Crédits

- Photographie de l'église Saint-Léger : Elke Wetzig, [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Cheylade,_%C3%89glise_Saint-L%C3%A9ger.jpg), licence CC BY-SA 4.0, image réduite.
- Blason du Cantal : dessin de Gretaz et contributeurs (Wikimedia Commons), licence CC BY-SA 3.0, image adaptée.
