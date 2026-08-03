# nexara-modpack

Modpack Fabric côté client pour le serveur **Nexara**, distribué et synchronisé automatiquement par [nexara-launcher](https://github.com/mayveen40-droid/nexara-launcher).

## Versions ciblées

| Composant       | Version   |
|-----------------|-----------|
| Minecraft       | 1.21.1    |
| Fabric Loader   | 0.19.3    |
| Pack (manifest) | voir `manifest.json` → `packVersion` |

## Fonctionnement

- `manifest.json` est lu par le launcher à chaque lancement (`updater.js`) pour savoir s'il doit télécharger une nouvelle version du pack.
- Le launcher compare `packVersion` du manifest à la version installée localement (`.installed-pack-version`) : si elles diffèrent, le zip pointé par `packUrl` est retéléchargé et extrait dans `mods/`.
- `zipSha256` (optionnel mais recommandé) permet au launcher de vérifier l'intégrité du zip téléchargé avant extraction.

## Publier une nouvelle version du pack

1. Mettre à jour les mods dans le dossier local, puis zipper le contenu en `modpack.zip`.
2. Créer une **Release GitHub** avec un tag `vX.Y.Z` (ex : `v1.1.0`) et y attacher `modpack.zip` en asset.
3. Le workflow `.github/workflows/update-manifest.yml` se déclenche automatiquement à la publication de la release : il calcule le SHA256 du zip, met à jour `manifest.json` (`packVersion`, `packUrl`, `zipSha256`) et commit le résultat sur `main`.
4. Si la version de Minecraft ou de Fabric Loader change, mettre à jour `mcVersion` / `fabricLoaderVersion` dans `manifest.json` manuellement avant de créer la release (le workflow ne touche pas ces deux champs).

## Mods inclus

_À compléter : liste des mods principaux du pack, pour s'y retrouver facilement lors des mises à jour._
