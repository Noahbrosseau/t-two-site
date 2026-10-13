# T-Two. — fiche de projet du site

Site du club de triathlon expérientiel **T-Two.** (Sherbrooke, Estrie).
Fondateurs : **Noah Brosseau** (expertise, kinésiologie) et **Luka Juneau** (création, image de marque).
Les deux peuvent demander des modifications à Claude. Ce fichier résume les décisions déjà prises : respecte-les, et demande avant d'en changer une.

## Publication

- Dépôt GitHub : `Noahbrosseau/t-two-site`, branche `main`.
- Netlify (compte de Luka, équipe « T-Two. », projet `t-two`) publie **automatiquement** chaque commit sur `main`, en environ 1 minute.
- Site : https://t-two.netlify.app · Déploiements : https://app.netlify.com/projects/t-two/deploys
- Aucun build : HTML statique. `netlify.toml` publie la racine (`.`).
- **Toujours** terminer chaque réponse à Noah par le lien du site en direct (https://t-two.netlify.app), même sans changement publié.
- Regroupe les petits changements en un seul commit quand c'est possible (chaque déploiement consomme des crédits Netlify).
- Messages de commit en français, courts et clairs.

## Structure

- `index.html` : tout le site (styles, contenu, script) dans un seul fichier.
- `media/` : vidéo et photos. **Temporaires** (prises au cellulaire), à remplacer par les versions pro.
  - `hero.mp4` (+ `hero-poster.jpg`) : vidéo de couverture, noir et blanc, 12 s en boucle.
  - `run.jpg`, `swim.jpg` : section « L'expérience ».
  - `luna.jpg` : partenaire Luna (gardée en couleur, c'est le produit).
- `confidentialite.html` : politique de confidentialité (Loi 25), FR et EN sur la même page (`#en` ouvre l'anglais). **Brouillon à faire valider** avant le lancement. Responsable : Noah Brosseau.
- `netlify.toml` : publication + en-têtes de sécurité (CSP, HSTS, X-Frame-Options…). Si tu ajoutes une ressource externe (script, police, image, iframe), mets la CSP à jour, sinon le navigateur la bloque.

### Où modifier quoi dans `index.html`

- **Textes** : objet `I` dans le script, avec `I.fr` et `I.en`. Toute modification de texte se fait **dans les deux langues**.
- **Événements** (dates, prix, lieux, horaires, places vendues) : tableau `EVENTS`. Chaque événement nourrit à la fois la ligne du temps, les dossards, le menu, sa page d'événement (`#launch`, `#backyard`…) et la billetterie.
- **Season Pass** : l'entrée `id:"pass"` dans `EVENTS`.
- **FAQ** : tableau `FAQ`.
- **Chrono du Launch** : constante `LAUNCH`.
- **Licence d'un jour Triathlon Québec** : constante `DAY_LIC` (13 $).
- **Couleurs et polices** : variables CSS dans `:root`, en haut du fichier.
- **Formulaires** : `#nForm` (infolettre, nom Netlify `infolettre`) et `#pForm` (partenaires, nom Netlify `partenaires`). Ce sont des Netlify Forms : HTML statique avec `data-netlify="true"`, champ caché `form-name`, piège à robots `adresse`, envoi en `fetch` vers `/`. Ne jamais les générer en JavaScript (Netlify ne les détecterait plus). Les envois arrivent dans Netlify → projet t-two → Forms.
- Le formulaire de **billetterie** ne doit **pas** envoyer ses données à Netlify : les données sensibles (date de naissance, contact d'urgence, décharge) iront à la plateforme de billetterie.

## Identité visuelle (décidée — ne pas changer sans demander)

- Nom : **T-Two.** (avec majuscule T et le point final). Slogan : **« La Zone de transition »** / « The Transition Zone ».
- Direction : journal personnel / magazine / documentaire, mais clair et précis. Couverture de magazine, numéros de page, légendes en italique.
- Fond **blanc cassé crème** (`--paper`), beaucoup d'espace. Touches de **charcoal** (`--ink`) et de dégradés « cliché de soleil » (`--dawn`, `--noon`, `--dusk`, `--night`, `--storm`).
- **Rythme crème / charcoal** (oct. 2026, équilibre entre Noah qui aime le crème et Luka qui aime le sombre) : le **sens** en charcoal (`class="dark"` : Éditorial, L'expérience, Notre histoire, pied de page), le **concret** en crème (couverture, Saison, Season Pass avec billet charcoal, Billetterie, Partenaires, FAQ). La classe `.dark` redéfinit les jetons de couleur localement : utilise toujours les variables, jamais de couleur codée en dur. Charcoal = `--charcoal` (#26282C), ni noir ni gris.
- Le **jaune** (`--flare`) seulement en petit éclat, au bon endroit. Le **corail** (`--coral`) pour les actions principales.
- Couleurs fixes : **pas de mode sombre**.
- Polices : Archivo (titres et texte), Newsreader italique (accents éditoriaux), IBM Plex Mono (étiquettes).
- Photos : traitement **noir et blanc cinématique** (contraste un peu relevé, grain léger, vignette). Exemple ffmpeg :
  `hue=s=0,eq=contrast=1.15:brightness=-0.02:gamma=0.96,noise=alls=6:allf=u`
- Dossards de course : chaque événement a sa date en très gros et 4 trous d'épingle, sur un **dégradé de couleur, sans photo** (décision de Noah, oct. 2026). Les 6 cartes ont **toutes la même taille** (2 rangées de 3 sur ordinateur) ; le Backyard garde seulement l'étiquette jaune « Défi signature ».
- Le logo actuel est **provisoire** (cercle à trois arcs). À remplacer par le logo vectoriel de Luka.

## Contenu et décisions

- Site **bilingue** FR/EN (bouton en haut). Traduction anglaise soignée, pas littérale.
- Barre du haut : liens, FR/EN, bouton Billets, menu ☰ plein écran (sections, 6 événements, 3 actions).
- Trois actions principales : acheter un billet, prendre le Season Pass, suivre sur Instagram.
- Saison 2027 : Launch Party, Café Ride, Sessions, Escape (Îles-de-la-Madeleine), Backyard (Lac-Stukely, Mont-Orford), Closing. **Prix et dates provisoires**, ajustés au dernier moment.
- Le Season Pass donne accès aux **6 événements**.
- **Luna** est Official Partner (niveau 2).
- Billetterie en 4 étapes : événement → billet (relais : noms des coéquipiers) → infos (contact d'urgence, date de naissance 18+, licence Triathlon Québec, t-shirt et allergies si pertinent) → décharge signée en ligne.
- Billetterie réelle visée : **Lepointdevente** (frais refilés à l'acheteur). Pour l'instant le formulaire ne prend pas de paiement.
- Le nombre de places restantes affiché est **un exemple** (`sold` dans `EVENTS`).
- Courriel affiché `bonjour@t-two.ca` : **à créer**. Pas encore de nom de domaine ni de @ Instagram final (les liens Instagram pointent vers instagram.com).

## Règles

- **Ne pas retirer** `<meta name="robots" content="noindex,nofollow">` avant que Noah ou Luka annonce le lancement public.
- Le site doit rester lisible sur téléphone (vérifier à environ 400 px de large).
- Pas de nouvelle bibliothèque ni de framework : rester en HTML/CSS/JS simple, un seul fichier.
- Garder les médias légers (vidéo de couverture sous ~4 Mo, photos sous ~300 Ko).
- Ne jamais inventer de partenaires, de témoignages ni de chiffres réels.

## À faire avant le lancement

- [ ] Logo vectoriel, photos des fondateurs, photos et vidéos pro
- [ ] Prix, dates et lieux finaux
- [ ] Nom de domaine + courriel T-Two
- [ ] Billetterie Lepointdevente reliée aux boutons « Réserver »
- [x] Infolettre et formulaire partenaires (Netlify Forms) — vérifier que la détection des formulaires est activée dans Netlify
- [x] Brouillon de politique de confidentialité (`confidentialite.html`)
- [ ] Faire valider la politique de confidentialité et la décharge
- [ ] Créer le courriel `bonjour@t-two.ca` (utilisé dans la politique et les messages d'erreur)
- [ ] Retirer le `noindex`, puis « Make public » dans Netlify
