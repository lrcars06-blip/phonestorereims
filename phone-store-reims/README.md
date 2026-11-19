# Phone Store Reims

Site vitrine de Phone Store, atelier de réparation smartphones et tablettes, galerie des Capucins, 7 rue des Capucins, 51100 Reims.

Site statique, sans dépendance ni étape de build : tout le code (HTML, CSS, JS) est dans `index.html`.

## Contenu du dossier

| Fichier | Rôle |
| --- | --- |
| `index.html` | Le site complet : intro animée, réparations, tarifs, prise de rendez-vous, adresse et horaires |
| `favicon.svg` | Icône de l'onglet |
| `README.md` | Ce document |
| `.gitignore` | Fichiers à ne pas versionner |

## Voir le site en local

Ouvrir `index.html` dans un navigateur. Aucun serveur n'est nécessaire.

## Mettre en ligne

### GitHub Pages

1. Pousser le dossier sur un dépôt GitHub (commandes ci-dessous).
2. Dans le dépôt : Settings, Pages, Source « Deploy from a branch », branche `main`, dossier `/ (root)`.
3. Le site est servi à `https://<utilisateur>.github.io/<depot>/` au bout d'une à deux minutes.

### Vercel

Importer le dépôt dans Vercel, Framework Preset « Other », sans commande de build ni dossier de sortie.

### Premier push

```bash
git init
git add .
git commit -m "Site Phone Store Reims"
git branch -M main
git remote add origin https://github.com/<utilisateur>/<depot>.git
git push -u origin main
```

## Ce qu'il faut régler avant la mise en ligne

Tout se trouve en haut du `<script>` de `index.html`, sous `CONFIGURATION`.

- **`TARIFS`** : les prix actuels sont des valeurs d'exemple. Les remplacer par la grille de la boutique. L'ordre des prix suit `REPARATIONS` ; `null` affiche « Sur devis ».
- **`BOUTIQUE.horaires`** : jours et heures d'ouverture (0 = dimanche, 6 = samedi, `null` = fermé). Les créneaux de rendez-vous, l'état ouvert/fermé et le tableau des horaires en découlent.
- **`BOUTIQUE.telIntl`** et **`BOUTIQUE.email`** : destinataires des demandes de rendez-vous.
- **Horaires écrits en dur** : deux lignes dans le téléphone de l'accueil (`.tel-horaires`) et le bloc JSON-LD dans le `<head>`.
- **Note Google** (`4,9/5 sur 1 277 avis`) : relevée en novembre 2026, à mettre à jour.
- **Mentions légales** : le lien du pied de page est vide.

## Prise de rendez-vous

Le formulaire compose un message pré-rempli et l'ouvre dans WhatsApp, l'appli SMS ou la messagerie du visiteur. La boutique confirme ensuite le créneau. Il n'y a pas de backend : deux visiteurs peuvent demander le même créneau.

Pour une réservation avec créneaux bloqués, remplacer le contenu de la fonction `envoyerDemande()` par un appel à une API (route Next.js, Cal.com, etc.). C'est le seul point d'entrée de l'envoi.

## Intro animée

- Jouée une fois par session de navigation.
- `?intro=1` dans l'URL la force à chaque chargement.
- Le lien « Revoir l'animation » du pied de page la relance.
- Désactivée pour les visiteurs qui ont activé « réduire les animations » dans leur système.
