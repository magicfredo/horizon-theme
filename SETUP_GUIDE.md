# Guide de Configuration - Développement Shopify

Ce guide résume la configuration effectuée et explique comment la reproduire sur n'importe quelle machine.

---

## 📋 Résumé de la configuration réalisée

### Ce qui a été installé et configuré :

1. **Shopify CLI** (v3.90.1)
   - Outil en ligne de commande pour gérer les thèmes Shopify
   - Authentification avec le compte : fmersseman@gmail.com

2. **Repository Git local**
   - Thème Horizon téléchargé depuis Shopify (411 fichiers)
   - Repository initialisé avec Git
   - `.gitignore` configuré pour exclure les fichiers sensibles

3. **Repository GitHub**
   - URL : https://github.com/magicfredo/horizon-theme
   - Branche principale : `main`
   - Code initial poussé avec 2 commits

4. **Structure du projet**
   ```
   /home/fmersseman/Projects/shopify/horizon-theme/
   ├── assets/          # CSS, JavaScript, images
   ├── blocks/          # Blocs réutilisables
   ├── config/          # Configuration du thème
   ├── layout/          # Layouts de base
   ├── locales/         # Traductions
   ├── sections/        # Sections modulaires
   ├── snippets/        # Code réutilisable
   ├── templates/       # Templates de pages
   ├── .gitignore       # Fichiers à ignorer
   └── README.md        # Documentation
   ```

---

## 🪟 Configuration sur Windows

### Prérequis

- Compte Shopify avec accès à une boutique
- Compte GitHub
- Terminal (PowerShell, CMD ou Git Bash)

---

### Étape 1 : Installer Node.js

**Windows :**

1. Téléchargez Node.js depuis https://nodejs.org/
2. Choisissez la version LTS (Long Term Support)
3. Lancez l'installeur et suivez les instructions
4. Vérifiez l'installation :
   ```powershell
   node --version
   npm --version
   ```

---

### Étape 2 : Installer Shopify CLI

**Windows (PowerShell en tant qu'administrateur) :**

```powershell
npm install -g @shopify/cli @shopify/theme
```

**Vérification :**
```powershell
shopify version
```

---

### Étape 3 : Installer Git

**Windows :**

1. Téléchargez Git depuis https://git-scm.com/download/win
2. Lancez l'installeur
3. Options recommandées lors de l'installation :
   - ✅ Git Bash
   - ✅ Git from the command line and also from 3rd-party software
   - ✅ Use Windows default console window

**Vérification :**
```powershell
git --version
```

**Configuration initiale :**
```powershell
git config --global user.name "Votre Nom"
git config --global user.email "votre-email@example.com"
```

---

### Étape 4 : Authentification Shopify

```powershell
shopify auth login
```

- Une page web s'ouvrira
- Connectez-vous avec votre compte Shopify
- Autorisez l'accès

---

### Étape 5 : Créer un dossier de projet

**Windows :**

```powershell
# Créer un dossier
mkdir C:\Projects\shopify
cd C:\Projects\shopify
```

---

### Étape 6 : Télécharger un thème Shopify

**Option A : Télécharger un thème existant**

```powershell
# Créer un dossier pour le thème
mkdir mon-theme
cd mon-theme

# Lister les thèmes disponibles
shopify theme list --store=votre-boutique.myshopify.com

# Télécharger le thème (remplacez l'ID par celui de votre thème)
shopify theme pull --store=votre-boutique.myshopify.com --theme=ID_DU_THEME
```

**Option B : Créer un nouveau thème depuis Dawn**

```powershell
shopify theme init mon-theme
cd mon-theme
```

---

### Étape 7 : Initialiser Git

```powershell
# Initialiser le repository
git init

# Créer un .gitignore
New-Item -Path .gitignore -ItemType File
```

**Contenu du `.gitignore` :**
```
# Config files with sensitive data
config/settings_data.json

# System files
.DS_Store
Thumbs.db

# IDE files
.vscode/
.idea/
*.sublime-project
*.sublime-workspace

# Node modules
node_modules/

# Environment variables
.env
.env.local

# Logs
*.log
npm-debug.log*

# Temporary files
*.tmp
*.temp
```

**Faire le premier commit :**
```powershell
git add .
git commit -m "Initial commit: Téléchargement du thème"
```

---

### Étape 8 : Créer un repository GitHub

**Option A : Via le site web**

1. Allez sur https://github.com/new
2. Nom du repository : `mon-theme`
3. Visibilité : Private (recommandé pour un projet commercial)
4. **Ne pas** cocher "Initialize with README"
5. Cliquez sur "Create repository"

**Option B : Via GitHub CLI** (plus rapide)

```powershell
# Installer GitHub CLI
winget install --id GitHub.cli

# Authentification
gh auth login

# Créer le repo
gh repo create mon-theme --private --source=. --remote=origin --push
```

---

### Étape 9 : Connecter Git et GitHub

**Si vous avez créé le repo manuellement (Option A) :**

```powershell
# Ajouter le remote
git remote add origin https://github.com/VOTRE-USERNAME/mon-theme.git

# Renommer la branche en main
git branch -M main

# Pousser le code
git push -u origin main
```

**Note :** GitHub vous demandera de vous authentifier :
- Username : votre nom d'utilisateur GitHub
- Password : utilisez un **Personal Access Token** (pas votre mot de passe)
  - Créez-en un sur https://github.com/settings/tokens
  - Permissions nécessaires : `repo`

---

### Étape 10 : Configuration SSH (optionnel mais recommandé)

**Pourquoi SSH ?**
- Plus sécurisé que HTTPS
- Pas besoin de retaper le mot de passe à chaque push

**Configuration :**

```powershell
# 1. Générer une clé SSH (dans Git Bash)
ssh-keygen -t ed25519 -C "votre-email@example.com"
# Appuyez sur Entrée pour accepter l'emplacement par défaut
# Créez un mot de passe (optionnel)

# 2. Afficher la clé publique
cat ~/.ssh/id_ed25519.pub
# Copiez tout le contenu

# 3. Ajouter la clé sur GitHub
# → https://github.com/settings/keys
# → "New SSH key"
# → Collez la clé
# → "Add SSH key"

# 4. Changer l'URL du remote
git remote set-url origin git@github.com:VOTRE-USERNAME/mon-theme.git

# 5. Tester
git push
```

---

## 🚀 Workflow de développement quotidien

### 1. Développer en local

```powershell
# Démarrer le serveur de développement
shopify theme dev --store=votre-boutique.myshopify.com

# Le thème sera accessible sur http://127.0.0.1:9292
```

**Avantages :**
- Voir les changements en temps réel
- Ne modifie PAS le site en ligne
- Parfait pour tester

### 2. Sauvegarder sur GitHub

```powershell
# Voir les fichiers modifiés
git status

# Ajouter les modifications
git add .

# Créer un commit
git commit -m "Description des modifications"

# Pousser sur GitHub
git push
```

### 3. Déployer sur Shopify

```powershell
# Pousser vers le thème live
shopify theme push --store=votre-boutique.myshopify.com

# OU pousser vers un thème de développement (recommandé)
shopify theme push --store=votre-boutique.myshopify.com --unpublished
```

**⚠️ Important :** `shopify theme push` modifie directement le thème sur Shopify !

---

## 🔄 Workflow avec branches Git (recommandé)

```powershell
# 1. Créer une branche pour une nouvelle fonctionnalité
git checkout -b feature/nouvelle-section

# 2. Faire vos modifications
# ... éditer des fichiers ...

# 3. Tester localement
shopify theme dev --store=votre-boutique.myshopify.com

# 4. Commiter
git add .
git commit -m "Ajout d'une nouvelle section produit"
git push origin feature/nouvelle-section

# 5. Créer une Pull Request sur GitHub
# → Permet de reviewer le code avant de merger

# 6. Merger dans main
git checkout main
git pull
git merge feature/nouvelle-section
git push

# 7. Déployer sur Shopify
shopify theme push --store=votre-boutique.myshopify.com
```

---

## 📝 Commandes Shopify CLI utiles

```powershell
# Authentification
shopify auth login
shopify auth logout

# Gestion des thèmes
shopify theme list --store=BOUTIQUE
shopify theme pull --store=BOUTIQUE
shopify theme push --store=BOUTIQUE
shopify theme dev --store=BOUTIQUE

# Options utiles
shopify theme push --unpublished          # Pousser vers un thème non publié
shopify theme push --theme=ID             # Pousser vers un thème spécifique
shopify theme dev --host=0.0.0.0          # Accessible depuis le réseau local
shopify theme dev --port=9293             # Changer le port

# Aide
shopify theme --help
shopify theme push --help
```

---

## 🛠️ Outils recommandés pour Windows

### Éditeur de code

**Visual Studio Code** (gratuit, recommandé)
- Téléchargement : https://code.visualstudio.com/
- Extensions utiles :
  - **Shopify Liquid** (syntax highlighting)
  - **GitLens** (visualisation Git avancée)
  - **Prettier** (formatage automatique)
  - **Auto Rename Tag** (HTML/Liquid)

**Alternatives :**
- Sublime Text
- Notepad++
- Atom

### Terminal

**Windows Terminal** (recommandé pour Windows 10/11)
- Téléchargement : Microsoft Store
- Supporte PowerShell, CMD, Git Bash, WSL

**Alternatives :**
- PowerShell 7
- Git Bash (inclus avec Git)
- ConEmu

### Git GUI (optionnel)

Si vous préférez une interface graphique :
- **GitHub Desktop** : https://desktop.github.com/
- **GitKraken** : https://www.gitkraken.com/
- **Sourcetree** : https://www.sourcetreeapp.com/

---

## 🔐 Sécurité - Bonnes pratiques

### ❌ Ne JAMAIS commiter :

- Tokens d'accès GitHub / Shopify
- Mots de passe
- Fichiers `.env` avec des secrets
- `config/settings_data.json` (peut contenir des données sensibles)

### ✅ À faire :

- Utiliser SSH au lieu de HTTPS pour GitHub
- Créer des tokens avec permissions minimales
- Révoquer les tokens exposés immédiatement
- Utiliser `.gitignore` correctement
- Ne jamais partager ses tokens publiquement

---

## 🆘 Problèmes courants et solutions

### Problème : "shopify: command not found"

**Solution :**
```powershell
# Fermer et rouvrir le terminal
# OU vérifier l'installation
npm list -g @shopify/cli
```

### Problème : Erreur d'authentification GitHub

**Solution :**
```powershell
# Utiliser un Personal Access Token
# https://github.com/settings/tokens
# Permissions : repo

# Ou configurer SSH (voir Étape 10)
```

### Problème : "Permission denied" lors du push Shopify

**Solution :**
```powershell
# Se reconnecter
shopify auth logout
shopify auth login
```

### Problème : Le serveur de dev ne se lance pas

**Solution :**
```powershell
# Vérifier que le port 9292 n'est pas utilisé
netstat -ano | findstr :9292

# Utiliser un autre port
shopify theme dev --port=9293
```

---

## 📚 Ressources

### Documentation officielle
- [Shopify Themes](https://shopify.dev/docs/themes)
- [Shopify CLI](https://shopify.dev/docs/api/shopify-cli)
- [Liquid Template Language](https://shopify.dev/docs/api/liquid)
- [Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com/)

### Tutoriels
- [Shopify Theme Development Course](https://www.shopify.com/partners/blog/topics/tutorials)
- [Git & GitHub for Beginners](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners)

### Communauté
- [Shopify Community Forums](https://community.shopify.com/)
- [Shopify Partners Slack](https://shopifypartners.slack.com/)

---

## 🎯 Checklist complète

### Configuration initiale

- [ ] Node.js installé
- [ ] Shopify CLI installé
- [ ] Git installé et configuré
- [ ] Compte Shopify accessible
- [ ] Compte GitHub créé
- [ ] SSH configuré (optionnel)
- [ ] Éditeur de code installé (VSCode recommandé)

### Pour chaque nouveau projet

- [ ] Authentification Shopify (`shopify auth login`)
- [ ] Dossier de projet créé
- [ ] Thème téléchargé ou créé
- [ ] Git initialisé (`git init`)
- [ ] `.gitignore` créé
- [ ] Premier commit effectué
- [ ] Repository GitHub créé
- [ ] Remote ajouté et code poussé
- [ ] README.md créé avec documentation

### Développement quotidien

- [ ] Créer une branche (`git checkout -b feature/...`)
- [ ] Développer et tester (`shopify theme dev`)
- [ ] Commiter régulièrement (`git add/commit`)
- [ ] Pousser sur GitHub (`git push`)
- [ ] Créer une PR pour review
- [ ] Merger dans main
- [ ] Déployer sur Shopify (`shopify theme push`)

---

## 💡 Conseils supplémentaires

### Organisation du code

1. **Commentez votre code** : Surtout dans Liquid, qui peut devenir complexe
2. **Utilisez des noms descriptifs** : Pour les sections, snippets, etc.
3. **Suivez les conventions Shopify** : Consultez les best practices

### Git

1. **Commits atomiques** : Un commit = une fonctionnalité/correction
2. **Messages clairs** : Décrivez ce qui a changé et pourquoi
3. **Branches descriptives** : `feature/`, `fix/`, `hotfix/`
4. **Pull souvent** : `git pull` avant de commencer à travailler

### Shopify

1. **Testez toujours en dev** : Avant de pousser en production
2. **Créez un thème de staging** : Pour tester les grosses modifications
3. **Backup régulier** : Téléchargez le thème live régulièrement
4. **Documentez les customizations** : Dans le README ou des commentaires

---

**Dernière mise à jour :** 2026-02-13

**Auteur :** Configuration réalisée avec Claude Code

---

## Questions fréquentes

**Q : Dois-je utiliser `shopify theme push` à chaque modification ?**
Non ! Utilisez `shopify theme dev` pour tester localement. `shopify theme push` uniquement quand vous voulez déployer en production.

**Q : Quelle est la différence entre GitHub et Shopify ?**
- **GitHub** = Sauvegarde et versioning de votre code
- **Shopify** = Hébergement et affichage du thème sur votre boutique
- Ce sont deux systèmes indépendants !

**Q : Puis-je travailler à plusieurs sur le même thème ?**
Oui ! C'est tout l'intérêt de Git/GitHub. Chaque personne travaille sur sa branche et crée des Pull Requests pour fusionner son travail.

**Q : Comment annuler une modification poussée sur Shopify ?**
Téléchargez une version précédente depuis Git et poussez-la avec `shopify theme push`.

**Q : Que faire si j'ai modifié le thème directement sur Shopify ?**
Faites `shopify theme pull` pour récupérer les changements, puis commitez-les sur Git.
