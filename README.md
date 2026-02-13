# Horizon Theme - The Whisky Factory

Thème Shopify personnalisé pour The Whisky Factory.

## À propos

Ce repository contient le thème Horizon utilisé pour la boutique Shopify [The Whisky Factory](https://the-whisky-factory.myshopify.com).

## Structure du projet

```
.
├── assets/          # CSS, JavaScript, images et icônes
├── blocks/          # Blocs réutilisables pour les sections
├── config/          # Configuration du thème
├── layout/          # Layouts de base (theme.liquid, password.liquid)
├── locales/         # Fichiers de traduction (multilingue)
├── sections/        # Sections modulaires
├── snippets/        # Morceaux de code réutilisables
└── templates/       # Templates de pages
```

## Développement local

### Prérequis

- [Shopify CLI](https://shopify.dev/docs/api/shopify-cli) installé
- Node.js
- Accès à la boutique Shopify

### Commandes utiles

```bash
# Prévisualiser le thème localement
shopify theme dev --store=the-whisky-factory.myshopify.com

# Pousser les modifications vers Shopify
shopify theme push --store=the-whisky-factory.myshopify.com

# Télécharger les dernières modifications depuis Shopify
shopify theme pull --store=the-whisky-factory.myshopify.com

# Lister les thèmes disponibles
shopify theme list --store=the-whisky-factory.myshopify.com
```

## Workflow de développement

1. **Créer une branche** pour vos modifications
   ```bash
   git checkout -b feature/ma-nouvelle-fonctionnalite
   ```

2. **Développer localement** avec preview en temps réel
   ```bash
   shopify theme dev --store=the-whisky-factory.myshopify.com
   ```

3. **Tester vos modifications** sur `http://127.0.0.1:9292`

4. **Commiter et pousser**
   ```bash
   git add .
   git commit -m "Description des modifications"
   git push origin feature/ma-nouvelle-fonctionnalite
   ```

5. **Créer une Pull Request** sur GitHub

6. **Déployer sur Shopify** une fois validé
   ```bash
   shopify theme push --store=the-whisky-factory.myshopify.com
   ```

## Ressources

- [Documentation Shopify Themes](https://shopify.dev/docs/themes)
- [Liquid Template Language](https://shopify.dev/docs/api/liquid)
- [Shopify CLI](https://shopify.dev/docs/api/shopify-cli)
- [Admin Shopify](https://the-whisky-factory.myshopify.com/admin)

## Sécurité

**IMPORTANT** : Ne jamais commiter :
- Les tokens d'accès
- Les fichiers `.env` avec des secrets
- Le fichier `config/settings_data.json` (contient des données sensibles)

Ces fichiers sont déjà listés dans `.gitignore`.

## License

Propriétaire - The Whisky Factory
