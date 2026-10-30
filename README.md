# DocReader Pro

Lecteur de documents **100 % hors-ligne** pour Android : PDF, Word (.docx/.doc), Excel (.xlsx/.xls/.csv),
PowerPoint (.pptx), texte, Markdown et JSON. Pas de publicité, pas de compte, pas de suivi — et l'application
ne déclare **aucune permission** (pas même INTERNET : voir `app/src/main/AndroidManifest.xml`).

## Obtenir l'APK

### Sans Android Studio (depuis un téléphone ou un PC)
1. Créez un dépôt GitHub (privé si vous voulez) et envoyez-y tout ce dossier.
2. Onglet **Actions** → « Construire l'APK » (il se lance tout seul à chaque envoi, ou via *Run workflow*).
3. Une fois terminé (~5 min), téléchargez l'artefact **DocReaderPro-apk** → `DocReaderPro.apk` → installez-le
   (autorisez « sources inconnues » pour votre navigateur / gestionnaire de fichiers).

### Avec Android Studio
Ouvrez ce dossier → *Run*. Le moteur web est déjà précompilé dans `app/src/main/assets/www`.
Pour le reconstruire après modification : `cd web && npm install && npm run build:android`.

## Fonctions
- **Bibliothèque** : reprise de lecture, favoris, filtres par type, tri, recherche, renommer/supprimer (annulable).
- **PDF** : défilement continu, zoom (pincement, double-tap, boutons), recherche surlignée, sommaire, liens internes,
  texte sélectionnable, mode sombre/sépia, curseur de page.
- **Word** : titres, listes, tableaux (cellules fusionnées), images, liens, notes de bas de page ; réglages de
  taille, police, interligne, marges. `.doc` ancien : texte seul.
- **Excel/CSV** : grille fluide même sur de gros classeurs, onglets, première ligne figée, formats de nombres/dates,
  recherche dans toutes les feuilles, détail et formule d'une cellule. `.xls` ancien : valeurs seules.
- **PowerPoint** : diapositives en cartes (titres, puces, tableaux, images, notes).
- **Signets** par document, sommaire, thèmes (auto, clair, sépia, sombre, noir), français/anglais.
- **Ouvrir avec…** depuis n'importe quelle appli, partage vers DocReader Pro, ouverture de dossiers entiers.

## Architecture
- `web/` : moteur de lecture (TypeScript, bundlé par esbuild, pdf.js + JSZip uniquement). Fonctionne aussi
  comme application web installable (`npm run build` → `web/dist`, avec service worker).
- `app/` : coque Android Kotlin minimale (WebView servie localement, sélecteur de fichiers/dossiers système).
- Les documents importés sont copiés dans le stockage privé de l'application (IndexedDB) ; l'original n'est jamais modifié.

## Limites connues
- Pas de remplissage de formulaires PDF ni d'annotations ; PDF protégés par mot de passe non pris en charge.
- Word : mise en page approximative (pas de pagination, en-têtes/pieds de page ignorés).
- La coque Kotlin n'a pas pu être compilée dans l'environnement où elle a été écrite : si Gradle signale une
  erreur, elle sera d'une ligne à corriger.

