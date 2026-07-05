# Romain MILLAN - Healthcheck

Générateur de page `_healthcheck` HTML autonome, au format BEM (`.rmh-*`),
avec ou sans le tag Romain MILLAN.

Initialement conçu pour les applications Laravel à des fins légales
(obligation de monitoring / preuve de disponibilité des services).

## Fonctionnement

Un push sur `main` déclenche une GitHub Action qui :
1. Télécharge le dernier `tag.css` depuis `RomainMILLAN/Romain-MILLAN-Tag`
2. Génère `_healthcheck.html` (avec tag) et `_healthcheck-without-tag.html` (sans tag)
3. Crée une Release GitHub avec les deux fichiers attachés

## Fichiers

| Fichier | Rôle |
|---|---|
| `build-healthcheck.sh` | Script de génération |
| `.github/workflows/build-healthcheck.yml` | CI : push → release |
| `_healthcheck.html` | Page complète BEM + tag Romain MILLAN |
| `_healthcheck-without-tag.html` | Page sans le tag |

## Installation sur un site

```bash
# Télécharger la dernière version depuis les Releases
curl -LO https://github.com/RomainMILLAN/Romain-MILLAN-Healthcheck/releases/latest/download/_healthcheck.html
```

Ou téléchargement manuel depuis l'onglet **Releases** de GitHub.

Dans une route Laravel :

```php
Route::get('/_healthcheck', function () {
    return response()->file(public_path('_healthcheck.html'));
});
```

## Personnalisation

- **Status up/down** : remplacer la classe `rmh-healthcheck--up` par `rmh-healthcheck--down` sur le bloc racine
- **Message** : modifier le texte dans `.rmh-healthcheck__message`
- **Titre** : modifier le texte dans `.rmh-healthcheck__title`

## Mise à jour du tag

Quand `RomainMILLAN/Romain-MILLAN-Tag` est mis à jour :
1. Pusher n'importe quoi sur `main`
2. La CI regénère les fichiers avec le nouveau CSS du tag
3. Télécharger les nouveaux fichiers depuis la dernière Release

## Build local

```bash
bash build-healthcheck.sh
```

Génère les deux fichiers dans le dossier courant.
