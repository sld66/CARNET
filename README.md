# Carnet

Bloc-notes personnel inspiré de OneNote : carnets, sections, pages, listes de tâches, images, recherche, mode sombre.
Il fonctionne dans le navigateur, sur ordinateur comme sur téléphone, même hors connexion, et se synchronise avec **Google Drive**.

Vos notes ne sont **jamais** envoyées sur GitHub. Elles restent sur vos appareils et dans votre Google Drive (dossier `Carnet`, fichier `carnet-notes.json`).

---

## Mise en ligne : 3 étapes (environ 20 minutes, une seule fois)

### Étape 1 : publier le site sur GitHub Pages

1. Connectez-vous sur **github.com**, puis cliquez sur **New repository**.
2. Nom : `carnet`. Visibilité : **Public** (obligatoire pour GitHub Pages avec un compte gratuit ; seul le code est visible, pas vos notes). Cliquez sur **Create repository**.
3. Sur la page du dépôt, cliquez sur **uploading an existing file**, puis faites glisser **tout le contenu** de ce dossier (y compris le dossier `icons`). Cliquez sur **Commit changes**.
4. Allez dans **Settings** puis **Pages**. Sous *Build and deployment* :
   - Source : **Deploy from a branch**
   - Branch : **main**, dossier **/ (root)**, puis **Save**.
5. Après une à deux minutes, votre site est à l'adresse : `https://VOTRE-PSEUDO.github.io/carnet/`

Notez cette adresse : vous en aurez besoin à l'étape 2.

### Étape 2 : autoriser la connexion à Google Drive (Google Cloud Console)

Cette étape donne à Carnet le droit de demander l'accès à votre Drive. C'est gratuit.

1. Ouvrez **console.cloud.google.com** avec votre compte Google.
2. En haut, dans le sélecteur de projet, cliquez sur **Nouveau projet**. Nom : `Carnet`. Cliquez sur **Créer**, puis sélectionnez ce projet.
3. Dans le menu **API et services**, puis **Bibliothèque**, cherchez **Google Drive API** et cliquez sur **Activer**.
4. Dans le menu **Google Auth Platform** (ou **API et services**, puis **Écran de consentement OAuth**), cliquez sur **Commencer** :
   - Nom de l'application : `Carnet` ; e-mail d'assistance : le vôtre
   - Cible : **Externe**
   - Coordonnées : votre e-mail. Acceptez les conditions, puis cliquez sur **Créer**.
5. Dans **Audience**, puis **Utilisateurs test**, cliquez sur **Add users** et ajoutez **votre adresse Gmail** (et celles de toute personne qui utilisera Carnet).
6. Dans **Clients**, cliquez sur **Créer un client** :
   - Type d'application : **Application Web**
   - Nom : `Carnet web`
   - **Origines JavaScript autorisées**, puis **Ajouter un URI** : `https://VOTRE-PSEUDO.github.io` (sans `/carnet` à la fin, sans `/` final)
   - Cliquez sur **Créer**.
7. Copiez l'**ID client**. Il ressemble à `123456789-abcdef.apps.googleusercontent.com`.

> Pas de panique si les libellés diffèrent légèrement : Google modifie régulièrement cette console. Les notions restent les mêmes : projet, API Drive activée, écran de consentement, client « Application Web » avec votre adresse GitHub comme origine.

### Étape 3 : coller l'ID client dans `config.js`

1. Sur GitHub, ouvrez le fichier `config.js` et cliquez sur le crayon (✏️ *Edit*).
2. Collez l'ID client entre les guillemets :
   ```js
   googleClientId: "123456789-abcdef.apps.googleusercontent.com"
   ```
3. Cliquez sur **Commit changes**. Une minute plus tard, c'est en ligne.

L'ID client n'est pas un mot de passe : il peut être public sans risque, car seule votre adresse GitHub est autorisée à l'utiliser.

---

## Utilisation

1. Ouvrez `https://VOTRE-PSEUDO.github.io/carnet/`.
2. En bas du menu des carnets, cliquez sur **Google Drive · non connecté**, puis sur **Se connecter à Google Drive**.
3. Google affiche *« Google n'a pas validé cette application »*. C'est normal pour une appli personnelle : cliquez sur **Continuer**, puis autorisez l'accès.
4. Faites de même sur chaque appareil : téléphone, ordinateur du bureau, tablette. Vous retrouvez partout les mêmes notes.

**Installer comme une application** (avec l'icône Carnet) :
- **Ordinateur (Chrome / Edge)** : icône « Installer » à droite de la barre d'adresse, ou bouton 📲 en bas du menu de Carnet.
- **Android (Chrome)** : menu ⋮, puis **Ajouter à l'écran d'accueil** ou **Installer l'application**.
- **iPhone / iPad (Safari)** : bouton Partager, puis **Sur l'écran d'accueil**.

### Bon à savoir

- **Hors connexion** : vous pouvez continuer à écrire. La synchronisation reprend toute seule au retour du réseau.
- **Modifications sur deux appareils en même temps** : Carnet fusionne page par page. Pour une même page modifiée des deux côtés, c'est la modification la plus récente qui l'emporte. Une page supprimée d'un côté part dans la corbeille de l'autre.
- **Reconnexion** : par sécurité, Google limite l'accès à une heure. Quand un bandeau *« Reconnectez Google Drive »* apparaît, un clic suffit. Vos notes restent enregistrées sur l'appareil en attendant.
- **Sauvegarde de secours** : le bouton ⬇ exporte toutes vos notes en JSON, et ⬆ les restaure.
- Le fichier `carnet-notes.json` du Drive ne doit pas être modifié à la main.

### Mettre à jour Carnet

Remplacez `index.html` sur GitHub par la nouvelle version, puis changez le numéro dans `sw.js` (`carnet-v1` devient `carnet-v2`). Les appareils récupèrent la nouvelle version à la prochaine ouverture.

---

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | L'application complète |
| `config.js` | Votre ID client Google (étape 3) |
| `manifest.webmanifest` | Nom et icônes pour l'installation |
| `sw.js` | Fonctionnement hors connexion |
| `icons/` | Logo et icônes |
