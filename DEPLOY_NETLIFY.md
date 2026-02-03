# Déploiement Netlify – résolution « Command was cancelled »

Si le build Gatsby **réussit** (~50 s) mais que le déploiement échoue avec :

- `Failed during stage 'building site': Command was cancelled`
- `Starting to deploy site from 'public'` → `Calculating files to upload` → **Execution cancelled**

la cause est en général le **plugin Essential Gatsby** ajouté automatiquement par Netlify. Pour un site statique (sans Gatsby Functions / DSG), ce plugin n’est pas nécessaire et peut provoquer cette annulation.

## Solution : désactiver le plugin Essential Gatsby

1. Ouvrir le **dashboard Netlify** : [https://app.netlify.com](https://app.netlify.com)
2. Sélectionner le **site** concerné
3. Aller dans **Site configuration** (ou **Build & deploy**) → **Build plugins** (ou **Plugins**)
4. Repérer **« Essential Gatsby »** / **« @netlify/plugin-gatsby »**
5. **Désactiver** le plugin (bouton **Disable** ou **Options** → Disable)
6. Déclencher un nouveau déploiement : **Deploys** → **Trigger deploy** → **Clear cache and deploy site**

Après désactivation, le build utilise uniquement la commande définie dans `netlify.toml` (`npm run build`) et le déploiement se fait normalement depuis le dossier `public/`.
