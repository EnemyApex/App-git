# GithubConnect

Application Android (Kotlin + Jetpack Compose) qui se connecte à ton compte GitHub
via un **Personal Access Token (PAT)** et affiche la liste de tes dépôts.

## Comment créer ton token GitHub

1. Va sur https://github.com/settings/tokens
2. **Generate new token** → **Generate new token (classic)**
3. Coche au minimum le scope `repo` (et `read:user` si tu veux ton nom/avatar)
4. Génère le token et copie-le (il ne sera affiché qu'une seule fois)

## Comment ouvrir et lancer le projet

1. Installe **Android Studio** (gratuit) : https://developer.android.com/studio
2. Ouvre le dossier `GithubConnect` (celui qui contient `settings.gradle.kts`) avec
   **File → Open**
3. Laisse Gradle synchroniser (ça télécharge les dépendances, nécessite Internet)
4. Lance l'app sur un émulateur ou un téléphone connecté (bouton ▶️ "Run")
5. Colle ton token dans l'écran de connexion

## Ce que fait l'app

- Écran de connexion : saisie du token GitHub
- Appel à `GET /user` et `GET /user/repos` de l'API GitHub (via Retrofit)
- Le token est sauvegardé de façon **chiffrée** sur l'appareil (EncryptedSharedPreferences),
  donc tu n'as pas besoin de le ressaisir à chaque ouverture
- Bouton "Déconnexion" pour effacer le token stocké

## Aller plus loin

- **OAuth complet** (à la place du token) : nécessite d'enregistrer une "OAuth App"
  sur GitHub (Settings → Developer settings → OAuth Apps), et d'ajouter un
  `CustomTabsIntent` + un `Activity` avec un `intent-filter` pour le callback
  (deep link `githubconnect://callback`). Dis-le-moi si tu veux que je l'ajoute.
- Ajouter les issues/PR : utiliser les endpoints `GET /repos/{owner}/{repo}/issues`
- Ajouter les notifications : endpoint `GET /notifications`

## Sécurité

Le token est stocké chiffré localement, mais reste sensible : ne partage jamais
ton token, et révoque-le sur GitHub si tu penses qu'il a fuité.
